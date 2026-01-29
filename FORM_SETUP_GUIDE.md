# Contact Form Email Setup Guide

This guide will help you receive form submissions via email at **wecarebd02@gmail.com**.

---

## 🎯 Recommended Solution: Formspree (Free & Easy)

### What You'll Get:
- Email notification for every form submission
- All form data included in the email
- Free tier: 50 submissions/month
- No coding required

### Setup Steps:

#### Step 1: Create Formspree Account
1. Go to [https://formspree.io/register](https://formspree.io/register)
2. Sign up using **wecarebd02@gmail.com**
3. Verify your email address

#### Step 2: Create Your Form
1. After login, click **"+ New Form"**
2. Give it a name: `WeCare Contact Form`
3. Formspree will generate a unique Form ID (looks like: `xyzabc123`)
4. Copy your form endpoint (looks like: `https://formspree.io/f/xyzabc123`)

#### Step 3: Update Your Website
1. Open `index.html` in your editor
2. Find line 196 where it says:
   ```html
   <form id="contactForm" class="contact-form" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```
3. Replace `YOUR_FORM_ID` with your actual Form ID from Formspree
4. Example:
   ```html
   <form id="contactForm" class="contact-form" action="https://formspree.io/f/xyzabc123" method="POST">
   ```
5. Save the file

#### Step 4: Test Your Form
1. Open your website
2. Fill out and submit the form
3. Check your email (wecarebd02@gmail.com) - you should receive the form data!

### What You'll Receive via Email:
Every time someone submits the form, you'll get an email with:
- Full Name
- Email Address
- Phone Number
- Service Date
- Preferred Callback Time
- Additional Information (if provided)

---

## 📧 Alternative: EmailJS (Also Free)

If you prefer EmailJS, here are the steps:

### Setup Steps:

#### Step 1: Create EmailJS Account
1. Go to [https://www.emailjs.com/](https://www.emailjs.com/)
2. Sign up and verify your email

#### Step 2: Add Email Service
1. In EmailJS dashboard, go to "Email Services"
2. Click "Add New Service"
3. Choose "Gmail"
4. Connect your wecarebd02@gmail.com account
5. Note your **Service ID**

#### Step 3: Create Email Template
1. Go to "Email Templates"
2. Click "Create New Template"
3. Use this template:

```
New Service Request from WeCare Website

Name: {{name}}
Email: {{email}}
Phone: {{phone}}

Service Date: {{serviceDate}}
Preferred Callback Time: {{callbackTime}}

Additional Information:
{{message}}
```

4. Note your **Template ID**

#### Step 4: Update Your Website

Add this script before the closing `</body>` tag in index.html:

```html
<script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
<script>
  // Initialize EmailJS
  emailjs.init('YOUR_PUBLIC_KEY'); // Get this from EmailJS dashboard

  // Update form submission
  const contactForm = document.getElementById('contactForm');
  contactForm.addEventListener('submit', function(e) {
    e.preventDefault();

    const submitBtn = this.querySelector('.submit-btn');
    submitBtn.textContent = 'Sending...';
    submitBtn.disabled = true;

    emailjs.sendForm('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', this)
      .then(function() {
        document.getElementById('formSuccess').classList.add('show');
        contactForm.reset();
        submitBtn.textContent = 'Submit Request';
        submitBtn.disabled = false;
      }, function(error) {
        alert('Failed to send. Please try again.');
        submitBtn.textContent = 'Submit Request';
        submitBtn.disabled = false;
      });
  });
</script>
```

Replace:
- `YOUR_PUBLIC_KEY` with your EmailJS public key
- `YOUR_SERVICE_ID` with your Service ID
- `YOUR_TEMPLATE_ID` with your Template ID

---

## 💰 Pricing Comparison

### Formspree
- **Free Tier:** 50 submissions/month
- **Basic:** $10/month - 1,000 submissions
- **Pro:** $40/month - 10,000 submissions

### EmailJS
- **Free Tier:** 200 emails/month
- **Personal:** $7/month - 1,000 emails
- **Professional:** $15/month - 5,000 emails

---

## ✅ Recommendation

**Use Formspree** because:
1. Easier to set up (just change one line of code)
2. No JavaScript library needed
3. Works even if JavaScript is disabled
4. Free tier is sufficient for most small businesses

---

## 🧪 Testing

After setup, test your form:
1. Fill out all required fields
2. Click "Submit Request"
3. Check your inbox at wecarebd02@gmail.com
4. You should receive an email within 1-2 minutes

### Troubleshooting:
- **Not receiving emails?** Check your spam folder
- **"Form not configured" error?** Make sure you replaced YOUR_FORM_ID
- **Form not submitting?** Check browser console for errors (Press F12)

---

## 📱 Form Data You'll Receive

Every submission will include:

```
Subject: New WeCare Service Request

From: noreply@formspree.io (or your EmailJS)

Body:
-----
Name: John Doe
Email: john.doe@example.com
Phone: +1 (480) 555-1234
Service Date: 2024-02-15
Preferred Callback Time: Morning (8:00 AM - 12:00 PM)
Additional Information: Need assistance for my elderly parent...
-----
```

---

## 🔒 Security Note

Both Formspree and EmailJS are secure services that:
- Use HTTPS encryption
- Protect against spam with reCAPTCHA (optional)
- Don't expose your email address in the website code
- Comply with GDPR and privacy regulations

---

## Need Help?

If you have any questions or issues:
1. Check the Formspree documentation: https://help.formspree.io/
2. Check the EmailJS documentation: https://www.emailjs.com/docs/
3. Or contact me for assistance!
