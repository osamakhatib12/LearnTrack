# 🧠 Osama Al-Khatib – Learning Progress Report

## 👨‍💻 Overview

This document summarizes my learning journey in programming, web scraping, backend development with Django, and an introduction to deep learning and cybersecurity. It reflects what I have already learned, what I’m currently focusing on, and my future learning plans and goals.

---

## ✅ What I've Learned So Far

### 🔹 Python Programming
- Mastered core Python: variables, loops, functions, conditionals, file handling.
- Used Python to write scripts for data extraction, JSON handling, and more.

### 🔹 Web Scraping
- Learned multiple scraping methods:
  - `requests` + `BeautifulSoup`
  - `requests-html` for rendering JS-based pages
  - `Selenium` for dynamic page interaction and scrolling
- Successfully scraped:
  - **OpenSooq** real estate listings with phone numbers
  - **OLX** & **Dubizzle** using DevTools and network requests
  - **Reddit** posts and comments using full automation with Selenium

---

## 📘 What I’m Currently Learning

### 🔹 Django (Backend Web Development)
- Project setup, virtual environments
- Models, Views, Templates (MVT)
- URL routing, forms, admin panel
- Preparing to build full-stack apps

### 🔹 Deep Learning (Intro)
- Basics of neural networks
- Watching Arabic tutorials on deep learning
- Understanding how models learn from data (classification, image, and text processing)

---

## 🔮 Future Plans and Goals

### 🔸 Django
- Learn advanced features (sessions, permissions, user auth)
- Build and deploy real-world web apps (e.g., dashboards, blog, API-based apps)

### 🔸 Deep Learning
- Study CNNs, RNNs, NLP models using Keras and TensorFlow
- Build smart models for image recognition or sentiment analysis
- Integrate DL models into Django apps

### 🔸 Cyber Security
- Apply my knowledge from the Cyber Shield Academy:
  - Network analysis, forensics, SOC monitoring, threat hunting
  - Ethical hacking and Python-based pentesting tools
- Build secure apps by implementing proper authentication, logging, encryption, and protection from web attacks (XSS, SQLi, CSRF)
- Explore AI-based cybersecurity solutions in the future

---

## 📚 Key Learning Resources

### Django
- [Django Arabic Course (YouTube)](https://www.youtube.com/playlist?list=PLp2eAGIFKMEVnAAJWhGzLc1Nn-tFP1UHP)
- [Django Documentation](https://docs.djangoproject.com/en/stable/)

### Deep Learning
- [Intro to Deep Learning – Arabic Course](https://www.udemy.com/course/intro-to-deep-learning-arabic/)
- [Deep Learning Specialization by Andrew Ng](https://www.coursera.org/specializations/deep-learning)

### Cyber Security
- Cyber Shield Academy (JODDB)
- SMT Security Training – CSA, EHA, DFIRA, SOC, Threat Hunter
- [TryHackMe](https://tryhackme.com), [Hack The Box](https://www.hackthebox.com/) – for hands-on labs

---

## 🏁 Final Thoughts

This roadmap is just the beginning of a long-term journey in tech, combining backend development, automation, AI, and security. I aim to build real-world projects, contribute to open source, and grow into a cybersecurity-aware developer with AI capabilities.
---

# 📄 Reddit Web Scraping Project – Technical Progress Report

**Project Owner**: Osama  
**Start Date**: May 2025  
**Goal**: Build a full-featured Reddit scraping system using Selenium, and evolve it into a professional portfolio project (for GitHub, LinkedIn, CV). Future integration with Django is planned.

## 🎯 Project Motivation
This project is more than a learning experience. It's a structured and scalable web scraping system built around Reddit. The motivation includes:
- Real-world challenge: Reddit has dynamic content, authentication, rate-limiting, nested data.
- Rich data variety: Posts, comments, replies, media, timestamps, etc.
- Evolving into a complete data pipeline with Django.

## ✅ Goals (Phase 1 - Web Scraping with Selenium)

### Core Technical Objectives:
- Use Selenium with ChromeDriver
- Implement auto-scroll to load all post/comment content
- Extract post-level data:
  - Username
  - Post title
  - Full post description (text + media + links)
  - Votes and comments count
  - Human-readable timestamps
- Extract all top-level comments:
  - Username
  - Full comment content (multi-type)
  - Time
  - Votes
- Extract replies (nested structure):
  - Track depth using `depth` attribute
  - Track identity using `comment-id` and `parent-id`
  - Detect whether a comment has replies using `div[slot="next-reply"]`
  - Detect hidden replies via "more replies" button
- Save post URLs to JSON file
- Save detailed post + comments + replies to structured JSON file
- Save progress file (for resume after crash / stopping)

### 🔧 Challenges Encountered & Solved:
- Post description not showing consistently -> Solved by dynamic parsing of `div[id*=post-rtjson-content]`
- Comments missing or repeated -> Solved by correct use of `.find_element` vs `.find_elements` + scrolling fixes
- Usernames showing `None` -> Fixed by using `get_attribute("author")`
- Votes/text not showing correctly -> Fixed by correct XPath + wait conditions
- Depth/Hierarchy confusion -> Solved with comment-id/parent-id based tree tracking

## 📁 Project Files Structure
- `Extract_Comments_And_Replies.py` -> main scraping logic
- `Functions_For_Scraping.py` -> helper: `slow_scroll()`
- `CommentsWithReplies.json` -> Final structured output
- `postLinks.json` -> URLs of posts collected for loop-based extraction

## 🔜 Next Steps (Upcoming Additions)
- Handle "More replies" button dynamically
- Support full recursion of replies (multi-depth nesting)
- Build a reply tree using comment-id and parent-id mapping
- Save replies inside `replies` array of each parent comment

## 🔄 Phase 2: Django Integration (Initial Planning)
- Learn Django basics in parallel
- Store Reddit post data in Django models
- Build a dashboard to explore scraped content
- Enable search, filter, and download from Django UI
- Secure API endpoints for the dataset

---

*Report Update Frequency*: This document will be updated daily with new progress, challenges, and design decisions.  
*Next update*: May 21, 2025  
*Prepared by*: ChatGPT - Technical Assistant to Osama



# ✅ Updates Added (May 26–27) 


### ✅ May 26–27 Reddit Comment Extraction Enhancements

1. 🧠 Improved detection of hidden and collapsed comments:
   - Recognized that some comments on Reddit remain hidden inside `<details>` tags or require scrolling/clicking to appear.
   - Adjusted logic to check for `shreddit-comment` components with `.collapsed` class, and detect when they change state to `open`.

2. 🔁 Nested reply handling and comment depth:
   - Structured comments using unique comment IDs and parent-child relationships.
   - Added logic to expand replies using buttons found inside `<slot name="next-reply">` or shadow DOM.
   - Ensured that even deeply nested replies (beyond level 3) are detected and stored correctly.

3. 🔄 Scroll-based full tree loading:
   - Triggered scrolling to load all top-level comments and check for `load more comments` buttons.
   - Supported handling of "more replies" dynamically loaded after expanding collapsed sections.

4. ✅ All improvements are now saved to structured JSON to maintain depth and reply order.




# ✅ Updates Added (May 28–29)

## 🔄 Project Updates – May 28–29, 2025

### 📅 5/28 – Dealing with Hidden Replies & External Permalinks
- Implemented detection logic for deep-level replies (depth=3) that have hidden "more replies" links pointing to separate permalink pages.
- Created a dedicated script `extract_more_reply_links.py` to:
  - Scroll and click all "show more replies" buttons dynamically using `smart_scroll_and_click()`.
  - Detect comments with `depth=3` and extract their `<a slot="more-comments-permalink">` URLs.
  - Avoid duplicates by checking `comment-id` against previously saved comments.
  - Save all collected links to `external_links.json`.
- Verified behavior with DevTools and screenshots to confirm the structure.

### 🛠️ Improvements on Smart Scrolling Logic
- Enhanced `smart_scroll_and_click()` to scroll dynamically and click on reply buttons reliably.

---

### 📅 5/29 – Merging Replies from External Pages
- Built the script `merge_external_replies.py` to:
  - Load collected external reply links.
  - Open each permalink page and run `extract_more_comments_and_replies_from_next_page()`.
  - Avoid duplication by:
    - Using a recursive `comment_id_exists()` function to deeply scan all comment trees.
    - Skipping new top-level comments that were previously replies (false top-level depth=0).
  - Correctly insert nested replies using the recursive `insert_comment_in_tree()` function.
  - Save merged output to `Updated_CommentsWithReplies.json`.

### 🐛 Bug Fixes & Validations
- Fixed an issue where some comment IDs were getting re-inserted as new top-level comments despite existing in reply trees.
- Confirmed proper merging of deeply nested replies by manually comparing JSON structure and UI.

### 🔍 Manual Verifications
- Used screenshots + comment tracing to validate:
  - Reply hierarchy (parent-id, depth, content).
  - Correct merge locations in the final output file.
  - No duplication after final patch.

---

## 📚 Recommended Learning Resources (Arabic) (باللغة العربية)

### 🟢 Django:
- **كورس Django الكامل بالعربي**: سلسلة شاملة لتعلم Django من الصفر حتى الاحتراف.  
  [مشاهدة الكورس](https://www.youtube.com/playlist?list=PLp2eAGIFKMEVnAAJWhGzLc1Nn-tFP1UHP)

- **Mastering Django in 2023 (Arabic)**: سلسلة تعليمية متقدمة لتعلم Django.  
  [مشاهدة السلسلة](https://www.youtube.com/watch?v=rJVQ7X77fxw)

### 🔵 Deep Learning:
- **دورة التحضير للتعلم العميق باللغة العربية**: دورة شاملة لتعلم Python والتعلم الآلي من الصفر.  
  [مشاهدة الدورة](https://www.udemy.com/course/machine-learning-and-deep-learning-for-arabs/)

- **Deep Learning MiniCamp [Arabic]**: دورة متقدمة في التعلم العميق باستخدام Keras وTensorFlow.  
  [مشاهدة الدورة](https://www.udemy.com/course/intro-to-deep-learning-arabic/)

- **مقدمة عن التعلم العميق باستخدام الماتلاب**: سلسلة فيديوهات تعليمية حول التعلم العميق باستخدام MATLAB.  
  [مشاهدة السلسلة](https://www.youtube.com/playlist?list=PLAI6JViu7XmflH_eGgsWkwvv6lbXhYjjY)
