# The Insider Challenges Walkthrough

---

## **The Insider-1**

**Description:**
Someone from our support team has leaked some confidential information. Can you find out who?

**Solution:**
This was the easiest one. I went to the support team page and saw **6 people** listed. I checked their Discord profiles one by one. When I opened **NoobMaster’s** profile, the flag was right there in the bio.

<img src="https://github.com/saxenatanishq/ScriptCTFCwriteups/blob/main/Osint/osint1.jpg" width="250" />

**Flag:**
`scriptCTF{1ts_0bv10u5ly_j0hn_d03_aka_n00bm4573r}`

---

## **The Insider-2**

**Description:**
You found the insider, but can you find what they leaked on GitHub and put it to use?

**Solution:**
This one was more interesting. In **NoobMaster’s** Discord bio, there were a lot of spaces, and then a hidden link appeared. It led to a login page. I needed credentials to log in.

<img src="https://github.com/saxenatanishq/ScriptCTFCwriteups/blob/main/Osint/osint2.jpg" width="250" />

I remembered that **NoobMaster’s GitHub** was linked on Discord. I found a repo called **scriptsorcerers-creds**. Inside, there was a file named **creds.txt** with:

<div>
	<img src="https://github.com/saxenatanishq/ScriptCTFCwriteups/blob/main/Osint/osint2a.jpg" width="250" style="display:inline-block; margin-right:10px;" />
	<img src="https://github.com/saxenatanishq/ScriptCTFCwriteups/blob/main/Osint/osint2b.jpg" width="250" style="display:inline-block;" />
</div>
scriptCTF2026:scriptCTF2026

I used these as the username and password to log in. After logging in, the flag was right there.

**Flag:**
`scriptCTF{scriptCTF_2026_leaked?!!}`

---

## **The Insider-3**

**Description:**
It's a tradition at this point. Continue where you left off...

**Solution:**
After logging in, I checked the page’s source code and found a link to this repo:
[scriptCTF/scriptCTF26/OSINT/leaked](https://github.com/scriptCTF/scriptCTF26/tree/main/OSINT/leaked)
I opened it, and the flag was right there in the repo.

<img src="https://github.com/saxenatanishq/ScriptCTFCwriteups/blob/main/Osint/osint3.jpg" width="250" />

**Flag:**
`scriptCTF{2026_fl4g_f0und_1n_2025}`

---

## **The Insider-4 (The Real Deal)**

**Description:**
Good luck! Note: The max flag limit is 6 for a reason—you should be able to get it in less than that.

**Solution:**
This was the actual challenge. Inside the **Insider-3** repo, there was a folder for **Insider-4**. It had a note and two attachments: **fireworks.jpg** and **room.jpg**.

### Step 1: Locate the Fireworks

I checked the **fireworks.jpg** comments and found a hidden message:
<img src="https://github.com/saxenatanishq/ScriptCTFCwriteups/blob/main/Osint/osint4.jpg" width="250" />
_"Great fireworks! Thanks to the Wendell family for organizing these!"_

A quick Google search revealed that the **Wendell family** is known for organizing fireworks in **Rockport, Texas**. So, the location was **Rockport, TX**.

### Step 2: Identify the Hotel

I opened **room.jpg**, which showed hotel rooms near the water. This meant a hotel by the sea or riverside. I used **Google Maps Street View** to search along the only street near the water. After some scrolling, I matched the hotel—**Days Inn by Wyndham Rockport Texas**.

<div>
	<img src="https://github.com/saxenatanishq/ScriptCTFCwriteups/blob/main/Osint/osint4a.jpg" width="250" style="display:inline-block; margin-right:10px;" />
	<img src="https://github.com/saxenatanishq/ScriptCTFCwriteups/blob/main/Osint/osint4d.jpg" width="250" style="display:inline-block;" />
</div>

### Step 3: Find the Room Number

The flag format was:
`scriptCTF{HOTEL_ADDRESS_ROOMNUMBER}`

The hotel address was **901 Hwy 35 N**. For the room number, I observed the room numbering style from Google Maps photos. Ground floor rooms started with **1xx**, and the first floor started with **2xx**. The room in the photo was on the ground floor.

<div>
	<img src="https://github.com/saxenatanishq/ScriptCTFCwriteups/blob/main/Osint/osint4c.jpg" width="250" style="display:inline-block; margin-right:10px;" />
	<img src="https://github.com/saxenatanishq/ScriptCTFCwriteups/blob/main/Osint/osint4b.jpg" width="250" style="display:inline-block;" />
</div>

I counted the rooms around the swimming pool—about **7 rooms before the pool** and **7 after**. Our room was on the right side, after the pool, so it had to be between **107–114**. Since the challenge allowed **6 tries**, I brute-forced it. After a few attempts, **111** worked!
<img src="https://github.com/saxenatanishq/ScriptCTFCwriteups/blob/main/Osint/osint4e.jpg" width="250" />

<div>
	<img src="https://github.com/scriptCTF/scriptCTF2025-OfficialWriteups/blob/main/OSINT/The%20Insider%204/numbers.png" width="250" style="display:inline-block; margin-right:10px;" />
	<img src="https://github.com/scriptCTF/scriptCTF2025-OfficialWriteups/blob/main/OSINT/The%20Insider%204/calculations.png" width="250" style="display:inline-block;" />
</div>

**Flag:**
`scriptCTF{901_Hwy_35_N_111}`

---

### **Final Thoughts**

**Insider-1 to 3** were warm-ups, but **Insider-4** was the real fun. It involved **EXIF data, Google Maps, guesswork, and brute-forcing** to crack it. A great challenge overall!
