# Task 3 – Integration Design

## Integration Flow

When a user submits the consultation form on the landing page, the information should first be sent to HubSpot using the **HubSpot Forms API**. I selected the Forms API because it is simple to integrate, reliable, and directly creates a lead in HubSpot without depending on third-party automation tools like Zapier or Make. Using the Forms API also gives better control over the data being sent from the website.

The form will send the user's Name, Phone Number, Source as **"Google Ads - Consultation Landing Page"**, and Lead Status as **"New Enquiry"**. Since this landing page collects only a phone number and not an email address, I would use the phone number to check whether the contact already exists in HubSpot. If a matching phone number is found, the existing contact will be updated instead of creating a duplicate record.

After the lead is successfully created, the system will trigger the **Karix WhatsApp Business API** to send a confirmation message to the patient. The message will inform the user that the enquiry has been received and that a clinic coordinator will contact them soon.

At the same time, **Google Tag Manager (GTM)** will capture the `consultation_form_submitted` event using `window.dataLayer.push()`. GTM will then forward this event to **Google Analytics 4** and **Google Ads**. This helps the marketing team measure conversions and understand which campaigns are generating genuine consultation requests.

## Biggest Failure Point

The biggest risk in this process is that the lead may not be created in HubSpot because of an API failure, internet issue, or temporary server problem. If this happens, the patient enquiry may not reach the CRM, which could result in a missed lead.

To reduce this risk, I would log every failed request, retry the API automatically after a short delay, and notify the support team if the request continues to fail after multiple attempts. This ensures that important enquiries are not lost.

## WhatsApp SLA Monitoring

The confirmation message should be delivered within two minutes after the form is submitted. Delays may happen because of API timeouts, network issues, or problems with the WhatsApp service provider. To monitor this, I would store the API response for every request, maintain logs for successful and failed deliveries, and generate an alert if a message is not delivered within the expected time. This allows the team to investigate the issue quickly and maintain a good user experience.