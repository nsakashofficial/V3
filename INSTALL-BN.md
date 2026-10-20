# MeetWoYou Functional Update v3 — বাংলা নির্দেশনা

## GitHub-এ আপলোড
1. আগে বর্তমান GitHub repository-এর একটি backup ZIP রাখো।
2. এই ZIP extract করো। ZIP-এর ভেতরের সব ফাইল সরাসরি repository root-এ upload করো—`dashboard.html`, `admin.html`, `messenger.html` যেই জায়গায় আছে সেই একই জায়গায়।
3. GitHub-এ **Commit changes** করো।
4. ১–৫ মিনিট পর সাইট খুলে Android Chrome-এ site data/cache clear করে আবার চালু করো। Service worker cache `mw-v12`-এ আপডেট হয়েছে।

## এই প্যাকেজে করা আসল পরিবর্তন
- Dashboard-এর header-এ Home settings gear সরিয়ে Profile section-এ Settings shortcut রাখা হয়েছে; Meetwoyou নাম মাঝখানে আছে।
- Post composer-এর emoji button এখন emoji picker খোলে এবং বেছে নেওয়া emoji লেখার মধ্যে বসায়।
- Video post-এর শুরুতে কৃত্রিম/random view count দেওয়া বন্ধ করা হয়েছে; নতুন post-এর view count শূন্য থেকে শুরু হয়।
- Admin-এর **Exit Admin** এখন শুধু login page-এ পাঠায় না—Firebase session sign out করে।
- Monetization policy-র Save button এখন `platformSettings/monetization` Firestore document-এ minimum payout, revenue share ও follower threshold save করে; admin খুললে saved values load হয়।
- Creator Studio-এর eligibility gate একই Firestore threshold পড়ে; default threshold 5,000 followers।
- Creator payout request balance deduction ও payout record-কে Firestore transaction-এ একসঙ্গে লেখে, এবং configured minimum payout যাচাই করে।
- Service worker cache version `mw-v12` করা হয়েছে এবং app-এর local modules cache shell-এ যোগ করা হয়েছে।

## গুরুত্বপূর্ণ সীমাবদ্ধতা / নিরাপত্তা
- Firestore rules-এ admin-only `platformSettings/monetization` write permission না থাকলে Save policy ব্যর্থ হবে। Error message দেখালে Firestore security rules যাচাই করতে হবে; শুধু frontend-এ admin email check-কে যথেষ্ট security ধরা যাবে না।
- Creator payout request কেবল `pending` request তৈরি করে এবং app balance reserve/deduct করে; এটি নিজে থেকে ব্যাংকে টাকা পাঠায় না। প্রকৃত পেমেন্টের জন্য নিরাপদ server-side/Cloud Function payout workflow দরকার।
- Firebase ও Cloudinary live account-এ end-to-end test করা যায়নি। Upload করার পর Login/Signup, feed, post, Messenger, profile, admin logout, policy save/load ও payout request আলাদাভাবে পরীক্ষা করবে।
