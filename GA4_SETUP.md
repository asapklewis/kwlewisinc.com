# Google Analytics 4 (GA4) Setup Instructions

## Overview
This document provides step-by-step instructions for implementing Google Analytics 4 (GA4) tracking on your static website.

## Prerequisites
- A Google Analytics account
- Access to your website's HTML files
- GA4 Measurement ID (format: G-XXXXXXXXXX)

## Step 1: Create GA4 Property

1. Go to [Google Analytics](https://analytics.google.com/)
2. Click "Admin" (gear icon in bottom left)
3. Under "Property" column, click "Create Property"
4. Enter property name and configure settings
5. Click "Create" and accept terms of service
6. Select "Web" as platform
7. Enter website URL and stream name
8. Click "Create stream"
9. Copy your **Measurement ID** (G-XXXXXXXXXX)

## Step 2: Add GA4 Tracking Code

Add the following code to the `<head>` section of **every HTML page** on your website:

```html
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

**Replace `G-XXXXXXXXXX` with your actual Measurement ID.**

## Step 3: Placement in HTML Files

For this project, add the tracking code to these files:

- index.html
- about.html
- contact.html
- services.html
- capability-statement.html
- request-consultation.html
- truth-series.html
- (any other HTML pages in your site)

**Important:** Place the code in the `<head>` section, before the closing `</head>` tag.

## Step 4: Verify Installation

### Real-Time Testing:
1. Visit your website
2. Go to GA4 dashboard
3. Click "Reports" → "Realtime"
4. You should see your visit appear within seconds

### Tag Assistant:
1. Install [Google Tag Assistant](https://tagassistant.google.com/)
2. Visit your website
3. Tag Assistant will show if GA4 is firing correctly

## Step 5: Configure Enhanced Measurement (Optional)

GA4 automatically tracks:
- Page views
- Scrolls
- Outbound clicks
- Site search
- Video engagement
- File downloads

To verify or configure:
1. Go to Admin → Data Streams
2. Click your web stream
3. Click "Enhanced measurement"
4. Enable/disable specific tracking options

## Step 6: Set Up Key Events (Optional)

Track important actions like:
- Form submissions
- Button clicks
- Consultation requests

### Example: Track Consultation Button Clicks

Add this code after your GA4 initialization:

```html
<script>
  // Track consultation button clicks
  document.addEventListener('DOMContentLoaded', function() {
    const consultBtn = document.querySelector('[href="request-consultation.html"]');
    if (consultBtn) {
      consultBtn.addEventListener('click', function() {
        gtag('event', 'consultation_request', {
          'event_category': 'engagement',
          'event_label': 'Consultation Button Click'
        });
      });
    }
  });
</script>
```

## Step 7: GitHub Pages Deployment

After adding GA4 code:
1. Commit changes to your repository
2. Push to `main` branch
3. GitHub Pages will automatically deploy
4. Wait 1-2 minutes for deployment
5. Visit your live site to test tracking

## Troubleshooting

### GA4 Not Tracking
- Verify Measurement ID is correct
- Check browser console for errors
- Ensure code is in `<head>` section
- Disable ad blockers during testing
- Wait 24-48 hours for full data population

### Multiple GA4 Tags Detected
- Remove any duplicate GA4 code
- Check for conflicting Google Tag Manager implementations

## Privacy Compliance

### Cookie Consent (if required)
- Implement cookie consent banner if targeting EU users
- Delay GA4 initialization until consent given
- Consider using Google Consent Mode

### Example Consent Implementation:

```html
<script>
  // Default consent state
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  
  gtag('consent', 'default', {
    'analytics_storage': 'denied'
  });
  
  // After user accepts cookies
  function acceptCookies() {
    gtag('consent', 'update', {
      'analytics_storage': 'granted'
    });
  }
</script>
```

## Best Practices

1. **Consistent Implementation**: Use same tracking code across all pages
2. **Test Before Launch**: Verify tracking in development environment
3. **Monitor Regularly**: Check GA4 dashboard weekly
4. **Data Retention**: Configure in Admin → Data Settings
5. **User Privacy**: Respect DNT (Do Not Track) signals when appropriate

## Additional Resources

- [GA4 Documentation](https://support.google.com/analytics/answer/10089681)
- [GA4 Event Reference](https://developers.google.com/analytics/devguides/collection/ga4/events)
- [Google Tag Manager](https://tagmanager.google.com/) (alternative implementation method)

## Support

For implementation questions:
- GA4 Help Center: https://support.google.com/analytics
- Google Analytics Community: https://support.google.com/analytics/community

---

**Last Updated:** February 2026  
**Version:** 1.0
