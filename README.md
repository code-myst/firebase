📚 ফায়ারবেস ফায়ারস্টোর শেখার সম্পূর্ণ সারসংক্ষেপ (Master Summary)

আমরা একদম শুরু থেকে ধাপে ধাপে ফায়ারবেস কনফিগারেশন, রিয়েল-টাইম ডাটাবেস অপারেশন এবং ডাটা ফিল্টারিং সম্পূর্ণ প্র্যাকটিক্যাল কোডের মাধ্যমে শিখেছি। নিচে সম্পূর্ণ বিষয়টির টেকনিক্যাল সামারি দেওয়া হলো:

🛠️ ১. ফায়ারবেস কানেকশন ও পরিবেশ প্রস্তুত করা

১. type="module": HTML-এ <script type="module"> ব্যবহার করতে হয় যেন ES6 import ব্যবহার করে CDN থেকে ফায়ারবেসের সার্ভিস আনা যায়।
২. initializeApp(firebaseConfig): প্রজেক্ট ক্রেডেনশিয়াল দিয়ে ফায়ারবেসের সাথে অ্যাপ কানেক্ট করা।
৩. getFirestore(app): ডাটাবেস হ্যান্ডেল করার জন্য db ইন্সট্যান্স বা রেফারেন্স তৈরি করা।

import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import { getFirestore } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);




🔄 ২. ফায়ারস্টোর CRUD এবং ফিল্টারিং ফাংশনগুলোর সারসংক্ষেপ

| কাজ (Operation) | ব্যবহৃত ফাংশন | কোড সিনট্যাক্স (Code Syntax) | মূল বৈশিষ্ট্য |
| ১. ডাটা সেভ (Auto ID) | addDoc | addDoc(collection(db, "col"), { data }) | ফায়ারবেস নিজে থেকে একটি র‍্যান্ডম ২-ক্যারেক্টারের ডকুমেন্ট আইডি তৈরি করে। |
| ২. রিয়েলটাইম রিড | onSnapshot | onSnapshot(collection(db, "col"), (snap) => {}) | ডাটাবেসে যেকোনো পরিবর্তন হলে পেজ রিলোড ছাড়াই ফ্রন্টএন্ড আপডেট হয়। |
| ৩. ডাটা ডিলিট | deleteDoc | deleteDoc(doc(db, "col", docId)) | নির্দিষ্ট docId ধরে ডাটাবেস থেকে ডকুমেন্ট মুছে ফেলে। |
| ৪. ডাটা সেভ/ওভাররাইট | setDoc | setDoc(doc(db, "col", customId), { data }) | ইউজার নিজের পছন্দমতো কাস্টম আইডি (যেমন: রোল/ইমেইল) ব্যবহার করতে পারে। |
| ৫. ফিল্ড আপডেট | updateDoc | updateDoc(doc(db, "col", docId), { key: val }) | ডকুমেন্টের বাকি ফিল্ড ঠিক রেখে শুধুমাত্র নির্দিষ্ট ফিল্ডের মান পরিবর্তন করে। |
| ৬. ডাটা ফিল্টার | query & where | query(colRef, where("topic", "==", "JS")) | নির্দিষ্ট শর্ত দিয়ে ফায়ারস্টোর থেকে ফিল্টার করা ডাটা টেনে আনে। |

💡 ৩. ধাপে ধাপে যা যা শিখেছেন (Code Snippets)

ক) অটো-আইডি দিয়ে ডাটা সেভ (addDoc)

import { collection, addDoc, serverTimestamp } from ".../firebase-firestore.js";

await addDoc(collection(db, "practice_collection"), {
    name: "রকিব",
    topic: "JS",
    createdAt: serverTimestamp() // গুগল সার্ভারের সঠিক টাইমস্ট্যাম্প
});




খ) লাইভ ডাটা ব্রাউজারে দেখানো (onSnapshot)

import { collection, onSnapshot } from ".../firebase-firestore.js";

onSnapshot(collection(db, "practice_collection"), (snapshot) => {
    snapshot.docs.forEach((docSnap) => {
        console.log(docSnap.id, docSnap.data()); // আইডি এবং অবজেক্ট ডাটা
    });
});




গ) নির্দিষ্ট ডাটা ডিলিট করা (deleteDoc)

import { doc, deleteDoc } from ".../firebase-firestore.js";

await deleteDoc(doc(db, "practice_collection", "DOCUMENT_ID"));




ঘ) কাস্টম আইডি দিয়ে সেভ করা (setDoc)

import { doc, setDoc } from ".../firebase-firestore.js";

await setDoc(doc(db, "practice_collection", "student_101"), {
    name: "সাকিব",
    topic: "React"
});




ঙ) নির্দিষ্ট ফিল্ড আপডেট করা (updateDoc)

import { doc, updateDoc } from ".../firebase-firestore.js";

await updateDoc(doc(db, "practice_collection", "DOCUMENT_ID"), {
    topic: "Next.js" // শুধু topic ফিল্ড আপডেট হবে
});




চ) শর্ত দিয়ে ডাটা ফিল্টার করা (query + where)

import { collection, query, where, onSnapshot } from ".../firebase-firestore.js";

const q = query(collection(db, "practice_collection"), where("topic", "==", "JS"));

onSnapshot(q, (snapshot) => {
    // শুধুমাত্র JS বিষয়ের ডাটা আসবে
});




🚀 ৪. ভবিষ্যতে শেখার পরবর্তী ধাপসমূহ (Next Steps)

১. Firestore Security Rules: ডাটাবেসের এক্সেস সুরক্ষিত করা (যেমন: allow read, write: if request.auth != null;)।
২. Firebase Authentication: ইউজারদের ইমেইল/পাসওয়ার্ড বা গুগল দিয়ে লগইন ও সাইন-আপ করানো।
৩. Composite Indexing: একই সাথে where এবং orderBy ব্যবহার করে ডাটা সর্ট ও ফিল্টার করা।
৪. Pagination (limit / startAfter): বড় কালেকশন থেকে ১০-২০টি করে ডাটা ধাপে ধাপে লোড করা।
