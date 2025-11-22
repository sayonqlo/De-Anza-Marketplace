# De-Anza-Marketplace
Scam resistant marketplace for De Anza students

## Inspiration
College students are frequent targets for scams on open platforms like Facebook Marketplace or Craigslist. We noticed that buying and selling textbooks, furniture, and electronics within the De Anza community was fragmented and risky. We wanted to create a safe, closed-loop economy where trust is established by default. Our inspiration came from wanting to merge the slick, easy-to-use interface of apps like Facebook Marketplace, Ebay, or Mercari with the institutional trust of a campus intranet.

## What it does
De Anza Marketplace is a localized, secure trading platform exclusively for De Anza College students.

Cybersecurity First Access: The app enforces a strict security gate. Users cannot view or post listings until they verify their identity via a 2-Factor Authentication (Magic Link) simulation tied to their @fhda.edu student email.

Secure Marketplace: Once verified, students can browse a real-time feed of items sold by their peers.

## How we built it
Frontend: We built the UI using HTML5 and Tailwind CSS. We focused on a clean, card-based, and mobile-responsive design to ensure it works great on phones while walking between classes.

Backend: Google Firebase

Firestore: Used for the real-time database. We structured it with public collections for marketplaceListings and private, secure collections for users to handle the verification data.

Authentication Logic: Since we couldn't connect to the live university SSO in the hackathon sandbox, we engineered a custom Mock 2FA Flow. We use Firebase Anonymous Auth to establish a session, then use Firestore documents to generate and validate 6-digit verification codes, effectively simulating a secure magic link system.

## Challenges we ran into
Simulating 2FA in a Sandbox: We wanted to prove the "Cybersecurity First" concept without having access to an email server. We had to creatively use Firestore listeners to simulate the "sending" and "receiving" of verification codes between the client and the database.

Session Persistence: Firebase's anonymous authentication is "sticky"—it remembers the user even after a refresh. This made testing different student IDs difficult. We solved this by implementing a hard reset on Logout that explicitly deletes the user's verification document from the database, forcing a fresh login state every time.

## Accomplishments that we're proud of
The Security Gate: We are most proud of the "Cybersecurity First" architecture. The marketplace UI is physically not rendered in the DOM until the verification state is confirmed true by the database.

Real-Time Interactivity: Seeing a listing pop up on one screen instantly after being posted on another device (without refreshing!) was a huge win.

## What we learned
Security UX: We learned that security adds friction (the login screen), but if you make the UI clean and the instructions clear ("Check your mock email box"), users are willing to trust the process.

## What's next for De Anza Marketplace
Real SSO Integration: Moving from our mock 2FA to actual integration with De Anza's Shibboleth/SAML login system.

In-App Chat: Replacing the "Contact Seller" placeholder with a real-time chat feature so students don't have to exchange phone numbers immediately.

Image Uploads: Implementing Firebase Storage to allow users to upload actual photos of their items instead of using placeholders.

Category Filters: Adding search and filtering to help students find specific textbooks or electronics faster.
