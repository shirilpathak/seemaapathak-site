# Payment Gateway Integration Guide

This guide shows you how to set up **Razorpay** and **Stripe** payment links for your astrology consultation services. The payment buttons on your website now support these providers.

---

## Quick Setup Summary

| Step | Time | Effort |
|---|---|---|
| 1. Choose provider (Razorpay recommended for India) | 5 min | Check fees & features |
| 2. Create merchant account | 10 min | Sign up & verify email |
| 3. Create Payment Link for your consultation prices | 10 min | Add prices ₹1,500, ₹2,100, ₹2,500 |
| 4. Copy payment link URL to website | 5 min | Paste URL in HTML |
| 5. Test payment (use test keys) | 10 min | Simulate a payment |
| **Total** | **~40 min** | **All free** |

---

## Option 1: Razorpay (RECOMMENDED for India) ⭐

### Why Razorpay?
- ✅ **UPI support** — Google Pay, PhonePe, Paytm, WhatsApp Pay (most popular in India)
- ✅ **Instant settlements** — Money in your bank within 2-3 hours
- ✅ **Lowest fees** — 2% + ₹0 (vs Stripe's 3.5% + ₹4 international fee)
- ✅ **INR convenient** — Prices in ₹, no currency conversion
- ✅ **Easy dashboard** — Intuitive UI for Indians
- ✅ **17+ payment methods** — Cards, wallets, NEFT, IMPS, banks

### Step 1: Create Razorpay Account
1. Go to https://razorpay.com/
2. Click **"Sign Up"** (top right)
3. Enter email & password
4. Verify email
5. Complete KYC (business/personal details)
   - Business name: "Seemaa Pathak Consultations" (or your business name)
   - Business category: "Professional Services" or "Consulting"
   - Your name, address, PAN (if available)
6. Activate account (takes 1-2 hours)

### Step 2: Create Your First Payment Link (Test Mode)
1. Go to **Dashboard** > **Payment Links** (left sidebar)
2. Click **"Create Payment Link"** (blue button)
3. Fill in details:
   - **Reference ID:** `consultation_45mins_career` (for your reference)
   - **Amount:** ₹2,100 (the consultation price)
   - **Description:** `Career & Business Consultation - 45 mins`
   - **Customer details (optional but good):**
     - Customer Name: Leave blank (customer enters at checkout)
     - Email: Leave blank
   - **Receipt ID:** `CAREER-2024-001` (optional)
   - **Notify:** Keep "Email" checked
   - **Notes:** `Vedic Astrology Consultation`

4. Click **"Create Link"**
5. **Copy the link** (looks like: `https://rzp.io/i/abcdef123456`)

### Step 3: Add Links to Your Website

**For services.html and contact.html:**

In the payment buttons area, find the `openPaymentModal` function. Replace:

```javascript
const paymentLinks = {
    razorpay: 'https://rzp.io/l/YOUR_RAZORPAY_PAYMENT_LINK_ID',
    // ... 
};
```

With your actual Razorpay link:

```javascript
const paymentLinks = {
    razorpay: 'https://rzp.io/i/YOUR_ACTUAL_LINK_CODE_HERE',
    // Example: 'https://rzp.io/i/0M4HpZhkP9'
    stripe: 'https://buy.stripe.com/test/YOUR_STRIPE_KEY'
};
```

[You only need the Razorpay link for now. Stripe is optional for international customers.]

### Step 4: Test Your Payment Link (Razorpay Sandbox)
1. Make sure you're still in **Test Mode** (toggle visible at top of Razorpay dashboard)
2. Click your payment link or the "Test" button in the Payment Links list
3. Test payment details:
   - **Phone:** Any 10 digit number (e.g., 9999999999)
   - **Email:** your email or test@gmail.com
   - **UPI ID:** Use one of these fake test IDs:
     - `success@razorpay` (will succeed)
     - `fail@razorpay` (will fail - to test decline)
   - OR select **Card** and use test card: `4111 1111 1111 1111`, any expiry/CVV
4. Click "Pay"
5. You should see a **success page**
6. Your test payment appears in the Dashboard > **Payments** list

### Step 5: Go Live (Switch from Test to Production)
1. **Production-ify your account:**
   - Razorpay will ask you to activate production mode
   - Accept Terms & Conditions
   - Choose your payment methods (we recommend: Cards, UPI, Wallets, Net Banking)

2. **Create Production Payment Links:**
   - DO NOT turn off test mode yet — keep test links for testing
   - Create NEW links in Production Mode:
     - ₹1,500 for 30-min (Numerology)
     - ₹2,100 for 45-min (Career, Relationship, Health)
     - ₹2,500 for 60-min (Spiritual Healing)
   - Copy **production** links and update your website

3. **Update your website** with production links:
   ```javascript
   const paymentLinks = {
       razorpay: 'https://rzp.io/i/PRODUCTION_LINK_HERE',
       stripe: 'https://buy.stripe.com/live/YOUR_STRIPE_LIVE_KEY'
   };
   ```

4. **Verify payment received:**
   - Customer pays via UPI/card
   - Check **Dashboard > Payments** to see the transaction
   - Money settles to your bank account within 1-2 hours

### Razorpay Fees
- **Cards (Credit/Debit):** 2% + ₹0
- **UPI:** 0% (FREE!)
- **Net Banking:** 0% (FREE!)
- **Wallets:** 0% (FREE!)

**Example:** For a ₹2,100 payment via UPI, you receive ₹2,100. For card, you receive ₹2,058 (2% fee).

### Support & Docs
- **Dashboard Help:** Click the "?" icon in Razorpay dashboard
- **Payment Link Docs:** https://razorpay.com/docs/payment-links/
- **Support Email:** support@razorpay.com or live chat in dashboard

---

## Option 2: Stripe (For International Customers & Cards)

### Why Stripe?
- ✅ Works globally — supports 135+ countries
- ✅ Best for cards — Visa, Mastercard, Amex
- ✅ Apple Pay & Google Pay natively supported
- ✅ Professional payment page
- ✗ **Higher fees** — 2.9% + $0.30 (for international, higher for INR cards)
- ✗ Requires business verification (takes 5-7 days)

### Step 1: Create Stripe Account
1. Go to https://stripe.com/
2. Click **"Start Now"** (top right)
3. Enter email & password
4. Set Business Country: **India** (or your country)
5. Business type: **Professional services** or **Consulting**
6. Verify email
7. Add bank account (for payouts)

### Step 2: Create a Payment Link
1. Go to **Products > Payment Links** (left sidebar)
2. Click **"Create"** (blue button)
3. Fill in:
   - **Product name:** `Career Consultation - 45 mins`
   - **Price:** Choose currency (INR for India, USD for international)
     - For INR: Enter ₹2,100
     - For USD: Enter $25 (approx equivalent)
   - **Billing period:** Select "One-time charge"
   - **Payment methods:** Check "Card" (and "Wallets" if available in your region)

4. Click **"Create link"**
5. **Copy the link** (looks like: `https://buy.stripe.com/test/abc123...`)

### Step 3: Add to Website
Same as Razorpay — find the `openPaymentModal` function and add your Stripe link.

### Step 4: Test
Use Stripe test card: `4242 4242 4242 4242` with any future date and any CVC.

### Stripe Fees
- **Domestic (India):** 2.9% + ₹4
- **International Cards:** 2.9% + $0.30

**Example:** For a ₹2,100 payment, you receive ₹2,037 (fee is ₹63).

---

## Option 3: PayPal (Alternative)

### Why PayPal?
- ✅ Widely trusted internationally
- ✅ Built-in buyer protection
- ✗ Higher fees — 2.9% + $0.30 globally
- ✗ Requires PayPal merchant account
- ✗ More complex setup

### Quick Setup
1. Create PayPal business account at https://www.paypal.com/in/
2. Go to **Tools > PayPal Buttons**
3. Create a payment button for each consultation type
4. Embed the button code in your website

[Full guide: https://www.paypal.com/in/webapps/mpp/how-to-get-started]

---

## Comparison Table: Razorpay vs Stripe vs PayPal

| Feature | Razorpay | Stripe | PayPal |
|---------|----------|--------|--------|
| **UPI Support** | ✅ Yes | ❌ No | ❌ No |
| **Cards** | ✅ Yes | ✅ Yes | ✅ Yes |
| **Net Banking** | ✅ Yes | ❌ No | ❌ No |
| **Wallets (Paytm, etc)** | ✅ Yes | ⚠️ Limited | ⚠️ Limited |
| **International** | ✅ Yes (expensive) | ✅ Best | ✅ Yes |
| **Fees (India)** | **2% cards, 0% UPI** | 2.9% + ₹4 | 2.9% + $0.30 |
| **Setup Time** | ~1 hour | 5-7 days (verification) | 1-2 hours |
| **Settlement** | 1-2 hours | 1-3 days | 1-2 days |
| **Dashboard** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Best For** | India domestic | Global/Cards | International |

**Recommendation:** Use **Razorpay** for Indian customers (0% UPI fees, instant settlement), keep Stripe as fallback for international cards.

---

## How to Update Your Website with Payment Links

### File: `services.html` and `contact.html`

Find this section in the HTML:

```html
<script>
function openPaymentModal(provider) {
    const paymentLinks = {
        razorpay: 'https://rzp.io/l/YOUR_RAZORPAY_PAYMENT_LINK_ID',
        stripe: 'https://buy.stripe.com/test/YOUR_STRIPE_PAYMENT_LINK_ID'
    };
    
    if (paymentLinks[provider]) {
        window.location.href = paymentLinks[provider];
    }
}
</script>
```

Replace with your actual links:

```html
<script>
function openPaymentModal(provider) {
    const paymentLinks = {
        razorpay: 'https://rzp.io/i/0M4HpZhkP9',  // Replace with your actual link
        stripe: 'https://buy.stripe.com/live/ExA_code'  // Replace with your actual link
    };
    
    if (paymentLinks[provider]) {
        window.location.href = paymentLinks[provider];
    } else {
        alert('Payment link not configured. Contact us at contact@seemaapathak.com');
    }
}
</script>
```

### Important: Test Thoroughly
1. After updating payment links, test by clicking the "Pay Now" buttons
2. Ensure you're redirected to the payment provider correctly
3. Test a real transaction with small amount to confirm everything works

---

## Next Steps (Future Phases)

### Phase 2 (When you want dynamic bookings):
- Instead of fixed payment links, create **server-side endpoints** to generate payment sessions
- Store booking details in a database
- Send confirmation emails after payment
- Implement webhooks for payment confirmation

### Phase 3 (Mobile App):
- Reuse the same payment APIs with React Native / Flutter
- Same Razorpay/Stripe integration works for both web and mobile

---

## Troubleshooting

### Payment button doesn't work / 404 error
- **Cause:** Payment link URL is broken or not copied fully
- **Fix:** Go back to Razorpay/Stripe dashboard, copy the link again, paste in HTML, save, and refresh page

### Payment succeeds but no email confirmation
- **Razorpay:** Check spam folder. Go to Dashboard > Emails to resend.
- **Stripe:** Same — check Emails section in dashboard

### Customer says payment failed but I see it in dashboard
- This can happen due to network delays. Check:
  - Razorpay: Dashboard > Payments (filter by date)
  - Ask customer to confirm their bank statement

### Settlement delayed
- **Razorpay test mode:** No actual settlement (it's test data)
- **Production:** Check banking hours (settle after 2 PM IST typically)

---

## Security Notes

✅ **Safe:** Your customers' card data goes directly to Razorpay/Stripe (not through your website)  
✅ **PCI Compliant:** Both providers handle compliance for you  
✅ **No secrets exposed:** Payment links don't contain sensitive keys  
❌ **Never:** Put API secret keys in your HTML or frontend code  

---

## Support & Resources

- **Razorpay Support:** https://support.razorpay.com
- **Stripe Support:** https://support.stripe.com/
- **PayPal Support:** https://www.paypal.com/in/smarthelp
- **Your Website:** Customers can email contact@seemaapathak.com or call +91 90000 00000 for payment issues

---

## Checklist: Getting Started

- [ ] Choose Razorpay ✓ (for India) or Stripe (for international)
- [ ] Create merchant account
- [ ] Create test payment links for each consultation type
- [ ] Test a payment with test credentials
- [ ] Create production payment links
- [ ] Update `services.html` with production links
- [ ] Update `contact.html` with production links
- [ ] Test production payment (real transaction if comfortable)
- [ ] Monitor dashboard for payments daily
- [ ] Commit changes to GitHub
- [ ] Share payment link with customers

---

**Ready to accept payments? Start with Razorpay in 30 minutes!** 🚀

