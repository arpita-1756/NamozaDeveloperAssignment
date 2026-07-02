# Task 1 – GTM Event Schema

## Introduction

Before running any Google Ads campaign, it is important to track the important actions that users perform on the website. These events help us understand user behaviour and measure how well the website is converting visitors into potential patients.


## GTM Event Schema

| Event Name | Trigger Type | Key Parameters | Used In |
|------------|--------------|----------------|----------|
| appointment_booking_started | Form Interaction | clinic_location, specialty, step_number | GA4 Funnel Exploration |
| booking_step_complete | Custom Event | step_number, step_name, clinic_location | GA4 Funnel Exploration |
| consultation_form_submitted | Form Submit | form_name, clinic_city, lead_source | Google Ads Conversion |
| call_now_clicked | Click | page_name, clinic_location, device_type | GA4 Events Report |
| whatsapp_chat_opened | Click | page_name, source, device_type | GA4 Engagement Report |
| patient_guide_downloaded | Form Submission + Download | guide_name, page_name, download_type | Downloads Report |
| clinic_page_view | Page View | clinic_name, city, page_title | Pages Report |
| blog_scroll_50 | Scroll | article_name, scroll_percentage, category | Engagement Report |
| blog_scroll_90 | Scroll | article_name, scroll_percentage, category | Engagement Report |



# Tracking the Booking Funnel

The appointment booking form has three steps. I would track every step separately using "window.dataLayer.push()" so that it becomes easy to find where users leave the booking process.

### Step 1

User selects:

- Clinic Location
- Specialty

After completing this step, a custom event is pushed to the dataLayer.

```javascript
window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 1,
  step_name: "location_specialty_selected",
  clinic_location: "Bengaluru",
  specialty: "Orthopaedic"
});
```

---

### Step 2

The user enters:

- Name
- Phone Number
- Preferred Date

After the details are entered successfully, another event is pushed.

```javascript
window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 2,
  step_name: "patient_details_entered",
  patient_name: "Rahul Sharma",
  phone: "9876543210",
  preferred_date: "2026-07-10"
});
```

---

### Step 3

Finally, when the booking is confirmed:

```javascript
window.dataLayer.push({
  event: "booking_confirmed",
  step_number: 3,
  booking_status: "confirmed",
  clinic_location: "Bengaluru",
  specialty: "Orthopaedic"
});
```

---

# Funnel Drop-off Tracking

Each booking step sends a different event to Google Tag Manager.

In Google Analytics 4 Funnel Exploration, I would create three funnel steps:

1. Location & Specialty Selected
2. Patient Details Entered
3. Booking Confirmed

This makes it easy to see where users leave the booking process. For example, if many users complete Step 1 but leave during Step 2, then the patient details form may need improvement.

---

# Google Ads Conversion

I would import "consultation_form_submitted" as the Google Ads conversion.

I selected this event because it shows that the user has successfully submitted the consultation form. This is the main goal of the landing page. Events like page views or button clicks only show interest, but a form submission shows that the visitor is actually interested in booking an appointment.