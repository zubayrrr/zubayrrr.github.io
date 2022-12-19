---
category: '2022'
created: 2022-12-19 14:30:01.524000+00:00
id: afdc6177-8608-4a5a-a42a-368df22abbcb
tags:
- devlog
- tidbits
title: Regex To Find
updated: 2022-12-19 14:30:02.332000+00:00
---
   
```regex
\b\d{2}/\d{2}/\d{2}\s\d{1,2}:\d{2}\s(?:AM|PM)\b
```
   
   
This regular expression will match strings that have the format "DD/MM/YY HH:MM AM or PM" It will match strings like "18/12/22 10:39 PM" and "18/12/22 8:00 PM", as well as any other string that follows this format.   
   
Explanation:   
   
   
-   `\b`: matches a word boundary   
-   `\d{2}`: matches two digits (e.g. 18)   
-   `/`: matches a forward slash   
-   `\d{2}`: matches two digits (e.g. 12)   
-   `/`: matches a forward slash   
-   `\d{2}`: matches two digits (e.g. 22)   
-   `\s`: matches a white space character   
-   `\d{1,2}`: matches one or two digits (e.g. 10 or 8)   
-   `:`: matches a colon   
-   `\d{2}`: matches two digits (e.g. 39 or 00)   
-   `\s`: matches a white space character   
-   `(?:AM|PM)`: matches either "AM" or "PM"   
-   `\b`: matches a word boundary   
   
Via — [ChatGPT](../devlog/ChatGPT.md)