const express = require('express');
const nodemailer = require('nodemailer');
const bodyParser = require('body-parser');
const crypto = require('crypto');

const app = express();
const port = 3000;

app.use(bodyParser.urlencoded({ extended: false }));
app.use(bodyParser.json());

// In-memory user storage (replace with a database in production)
const users = [];

app.get('/', (req, res) => {
  res.sendFile(__dirname + '/index.html');
});

// POST endpoint to send OTP via email
app.post('/sendOTP', (req, res) => {
  const { email } = req.body;

  // Check if the email exists in the user storage
  const user = users.find(u => u.email === email);
  if (!user) {
    return res.status(404).send('User not found');
  }

  // Generate a random 6-digit OTP
  const otp = Math.floor(100000 + Math.random() * 900000);

  // Save the OTP in the user object
  user.otp = otp;

  // Send OTP via email
  const transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
      user: 'your-email@gmail.com',
      pass: 'your-email-password',
    },
  });

  const mailOptions = {
    from: 'your-email@gmail.com',
    to: email,
    subject: 'Password Reset OTP',
    text: Your OTP for password reset is: ${otp},
  };

  transporter.sendMail(mailOptions, (error, info) => {
    if (error) {
      console.log(error);
      res.status(500).send('Error sending OTP');
    } else {
      console.log('Email sent: ' + info.response);
      res.status(200).send('OTP sent successfully');
    }
  });
});

// POST endpoint to reset password
app.post('/resetPassword', (req, res) => {
  const { email, otp, newPassword } = req.body;

  // Check if the email exists in the user storage
  const user = users.find(u => u.email === email);
  if (!user) {
    return res.status(404).send('User not found');
  }

  // Validate OTP
  if (user.otp !== otp) {
    return res.status(401).send('Invalid OTP');
  }

  // Update the password in the user object (replace with database update logic)
  user.password = newPassword;

  res.status(200).send('Password reset successfully');
});

app.listen(port, () => {
  console.log(Server is running at http://localhost:${port});
});