# GET और POST दोनों methods के वेब एप्लिकेशन में ज्यादातर इस्तेमाल होने वाले, vulnerable endpoints की पूरी लिस्ट नीचे दी जा रही है। हर एक endpoint ऐसा है जहां payload inject करके vulnerability चेक की जा सकती है।

## GET और POST method को समझने के लिए नीचे आसान भाषा और उदाहरण के साथ वर्णन किया गया है:

## GET Method क्या है?
- GET HTTP request method है, जिसका उपयोग सर्वर से डेटा **मंगाने (retrieve)** के लिए किया जाता है।
- इसमें डेटा URL के अंत में query parameters की तरह भेजा जाता है, जो सभी को दिखता है।
- GET request से भेजा गया डेटा ब्राउज़र के ऐड्रेस बार में भी दिखाई देता है, इसलिए यह कम सुरक्षित होता है।
- इसे मुख्य रूप से तब इस्तेमाल किया जाता है जब हमें सिर्फ कोई जानकारी प्राप्त करनी हो, जैसे वेबसाइट पर search करना।

### GET का उदाहरण:
```html
<form method="get" action="search.php">
  <label>Search:</label>
  <input type="text" name="query">
  <input type="submit" value="Search">
</form>
```
अगर user "book" लिखकर submit करता है, तो URL ऐसा दिखेगा:  
`search.php?query=book`

## POST Method क्या है?
- POST HTTP request method है, जिसका उपयोग सर्वर पर डेटा **सबमिट करने** के लिए किया जाता है, जैसे forms भरना।
- इसमें डेटा HTTP request body के अंदर भेजा जाता है, जो URL में नहीं दिखता, इसलिए यह ज्यादा सुरक्षित माना जाता है।
- POST method का उपयोग तब किया जाता है जब हमें संवेदनशील जानकारी (जैसे पासवर्ड) भेजनी हो या बड़ी मात्रा में डेटा सर्वर पर भेजना हो।

### POST का उदाहरण:
```html
<form method="post" action="login.php">
  <label>Username:</label>
  <input type="text" name="username">
  <label>Password:</label>
  <input type="password" name="password">
  <input type="submit" value="Login">
</form>
```
डेटा URL में नहीं दिखेगा, बल्कि सर्वर को सुरक्षित तरीके से भेजा जाएगा।

## GET और POST का मुख्य अंतर (सारांश)

| विशेषता             | GET Method                                   | POST Method                                  |
|----------------------|-----------------------------------------------|----------------------------------------------|
| डेटा कहाँ भेजा जाता है | URL के query parameter में                     | HTTP request body में                        |
| डेटा की सीमा           | छोटा, लगभग 2000 characters तक                | ज्यादा, बड़ा डेटा भी भेजा जा सकता है           |
| सुरक्षा                | कम सुरक्षित, डेटा URL में दिखाई देता है         | ज्यादा सुरक्षित, डेटा URL में नहीं दिखता        |
| उपयोग                 | डेटा प्राप्ति जैसे search, filter, pagination  | फॉर्म सबमिट, लॉगिन, रजिस्ट्रेशन, फाइल अपलोड        |
| कैशिंग               | कैश हो सकता है                             | कैश नहीं होता                                  |
| बुकमार्किंग            | URL बुकमार्क की जा सकती है                  | बुकमार्क नहीं किया जा सकता                      |

---
# GET Method Endpoints

- Search bar input (search?q=payload)[1]
- URL parameters (product?id=payload)
- Pagination (page=payload)
- Sorting/filtering (sort=payload, filter=color)
- Profile/user IDs (profile?id=payload)
- Download file (download?id=payload)
- Token/activation links (activate?token=payload)
- Product/license keys (key=payload)
- Redirect URLs (redirect=url/payload)
- API GET endpoints (api/data?id=payload)
- Category selection (category=payload)
- Item chooser (item=payload)
- Report/view IDs (view=payload)
- Location/region selection (location=payload)
- GET-based login (sometimes used for SSO: login?user=payload)[2]
- Image/file fetchers (image?id=payload)
- Query strings on forms (form?next=payload)
- Language/locale settings (lang=payload)
- Any endpoint with querystrings accepting user input

# POST Method Endpoints

- Login form (username=password)
- Registration form (username, email, password, address)
- Comment forms (comment=payload)
- Feedback, contact forms (message=payload)
- Password reset forms (new_password, confirm)
- File upload (file=payload)
- API POST endpoints (JSON, form-urlencoded data)
- Profile update forms (name, photo, bio, etc.)
- Settings/preferences submission (setting=payload)
- Payment checkout (amount, card, address)
- Blog/post creation (content=payload)
- Review submission (review=payload)
- Survey/questionnaire (answer=payload)
- Shopping cart checkout (cart_items, shipping info)
- New product/service submissions (details=payload)
- Any custom POST action—invite, approve, delete, update, etc.
- Multi-part form-data endpoints (photo, docs)
- Request bodies for updates/deletions (user update, remove item API)[1][2]

## Extra (GET/POST Both)

- Hidden input fields (can be manipulated)
- Cookies और custom HTTP headers (User-Agent, Referer)
- RESTful API endpoints for create/update/delete[2]
- Nested form-data fields (JSON/XML inputs)

[1](https://www.hackthebox.com/blog/5-common-web-attacks)
[2](https://www.vaadata.com/blog/how-to-strengthen-the-security-of-your-apis-to-counter-the-most-common-attacks/)
