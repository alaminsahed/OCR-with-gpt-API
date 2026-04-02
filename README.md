# 🖼️ Image Processing API with OpenAI

This project is a simple Node.js and Express API that allows users to upload images, process them using OpenAI, and receive structured JSON data describing the images.

---

## 🚀 Features

- Upload multiple images up to 10 files
- Convert uploaded images to Base64
- Send images to OpenAI for analysis
- Extract structured JSON from the AI response
- Automatically delete uploaded files after processing

---

## 📦 Tech Stack

- Node.js
- Express.js
- Multer
- OpenAI API
- dotenv

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd <your-project-folder>
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up environment variables

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_openai_api_key_here
```

---

## ▶️ Run the Server

```bash
node server.js
```

The server will run at:

```text
http://localhost:5000
```

---

## 📡 API Endpoint

### `POST /upload`

Upload images and get JSON data in response.

#### Request

- Method: `POST`
- Content-Type: `multipart/form-data`
- Field name: `images`
- Maximum files: `10`

#### Example using cURL

```bash
curl -X POST http://localhost:5000/upload \
  -F "images=@image1.jpg" \
  -F "images=@image2.jpg"
```

---

## 📤 Example Response

```json
{
  "data": {
    "objects": [
      {
        "name": "cat",
        "description": "A small white cat sitting on a sofa"
      }
    ]
  }
}
```

---

## 🧠 How It Works

### 1. Upload Images

The API uses `multer` to temporarily store uploaded files in the `uploads/` folder.

### 2. Convert Images to Base64

```js
fs.readFileSync(imagePath).toString("base64");
```

### 3. Send Images to OpenAI

- Each image is converted into a Base64 data URL
- The request is sent to the `gpt-4o-mini` model

### 4. Extract JSON from the Response

The API expects the model to return JSON wrapped inside a Markdown code block such as:

```json
{
  "key": "value"
}
```

### 5. Error Handling
- Returns 400 if no files are uploaded
- Returns 500 if image processing fails
- Throws an error if the OpenAI response does not contain valid JSON

## 🔒 Notes
- Make sure your OPENAI_API_KEY is valid
- Uploaded files are deleted after processing
- The current JSON extraction logic assumes the model returns JSON inside a fenced code block
- The current implementation builds image URLs as data:image/jpeg;base64,... for all files

## 📌 Future Improvements
- Add file type validation
- Add file size limits
- Support PNG, WebP, and other formats more explicitly
- Improve JSON extraction with fallback handling
- Add request validation and better error messages
- Add authentication and rate limiting
- Add Docker support
