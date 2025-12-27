<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Deal ni Deal x 7G17: MRP Dashboard</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Deal ni Deal & 7G17 Partnership: Marginal Revenue Product Analysis</h1>
    </header>
    <section>
        <form id="mrpForm">
            <label>Input Labor Units: <input type="number" id="labor" min="1" required></label>
            <label>Marginal Product (MP): <input type="number" id="mp" min="0" step="0.01" required></label>
            <label>Marginal Revenue (MR): <input type="number" id="mr" min="0" step="0.01" required></label>
            <button type="submit">Add Data Point</button>
        </form>
        <button id="emailReport">Email MRP Report</button>
        <div id="googleDocsUpdate">
          <a href="https://docs.google.com/document/d/your-google-doc-id" target="_blank">
            Check out or update the latest report on Google Docs
          </a>
        </div>
    </section>
    <section>
        <h2>MRP Variation Table</h2>
        <table id="mrpTable">
            <thead>
                <tr>
                    <th>Labor Units</th>
                    <th>Marginal Product</th>
                    <th>Marginal Revenue</th>
                    <th>Marginal Revenue Product (MRP)</th>
                </tr>
            </thead>
            <tbody>
                <!-- Data goes here -->
            </tbody>
        </table>
    </section>
    <script src="script.js"></script>
const mrpTableBody = document.querySelector('#mrpTable tbody');
const mrpData = [];

document.getElementById('mrpForm').onsubmit = function(e) {
    e.preventDefault();
    const labor = Number(document.getElementById('labor').value);
    const mp = Number(document.getElementById('mp').value);
    const mr = Number(document.getElementById('mr').value);
    const mrp = mp * mr;
    mrpData.push({ labor, mp, mr, mrp });
    renderTable();
    this.reset();
};

function renderTable() {
    mrpTableBody.innerHTML = '';
    mrpData.forEach(row => {
        mrpTableBody.innerHTML += `
            <tr>
                <td>${row.labor}</td>
                <td>${row.mp}</td>
                <td>${row.mr}</td>
                <td>${row.mrp.toFixed(2)}</td>
            </tr>
        `;
    });
}

// Placeholder for Nodemailer (email) integration
document.getElementById('emailReport').onclick = function() {
    // Here you'd send a POST request to your Node.js backend which uses Nodemailer
    fetch('/api/send-mrp-report', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ data: mrpData })
    })
    .then(res => res.json())
    .then(msg => alert(msg.status || "Report sent!"))
    .catch(err => alert('Failed to send email: ' + err.message));
};
const express = require('express');
const bodyParser = require('body-parser');
const nodemailer = require('nodemailer');
const app = express();

app.use(bodyParser.json());

const transporter = nodemailer.createTransport({
    service: 'gmail', // or another SMTP provider
    auth: {
        user: 'your.email@gmail.com',
        pass: 'your_app_password'
    }
});

app.post('/api/send-mrp-report', (req, res) => {
    const mrpRows = req.body.data || [];
    const html = `
        <h3>MRP Data Report</h3>
        <table border="1" cellpadding="4" style="border-collapse: collapse;">
          <tr><th>Labor</th><th>MP</th><th>MR</th><th>MRP</th></tr>
          ${mrpRows.map(r => `<tr>
            <td>${r.labor}</td><td>${r.mp}</td><td>${r.mr}</td><td>${r.mrp}</td>
          </tr>`).join('')}
        </table>
    `;
    transporter.sendMail({
        from: '"Deal ni Deal Reports" <your.email@gmail.com>',
        to: 'recipient@example.com', // change to your team/email
        subject: 'Marginal Revenue Product Data',
        html
    }, (err, info) => {
        if (err) return res.json({ status: "Email send failed" });
        res.json({ status: 'Report sent!' });
    });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log('Nodemailer server running on port', PORT));
</body>
</html>