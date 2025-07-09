# 🔐 Face Blur Magic

Protect your privacy with AI-powered face detection and blurring.  
This project uses a **FastAPI backend** to detect faces and apply a blur, and a beautifully animated **HTML/CSS/JS frontend** to provide a smooth user experience.

---

## 🌟 Features

- 📸 Upload images with faces
- 🧠 AI detects faces and blurs them using OpenCV
- 🎨 See **Before/After** results
- 💻 FastAPI backend with `/process` endpoint
- 💅 Stylish and responsive frontend with animations

---

## 🚀 Live Demo

Try it on **Hugging Face Spaces**:  
👉 [https://krrishcoder07-face-blur-app.hf.space](https://krrishcoder07-face-blur-app.hf.space)

---

## 🗂 Project Structure

```
face-blur-magic/
├── backend/
│   ├── main.py              # FastAPI logic
│   └── requirements.txt     # Python dependencies
├── frontend/
│   ├── index.html           # UI markup
│   └── style.css            # All styles and animation
├── README.md                # You're here!
```

---

## 🧠 Tech Stack

- **Frontend**: HTML, CSS, JavaScript
- **Backend**: FastAPI, OpenCV, RetinaFace
- **Deployment**: Hugging Face Spaces

---

## 🛠️ Backend Setup (FastAPI + OpenCV)

### 1. Clone the repo

```bash
git clone https://github.com/krrishcoder07/face-blur-magic.git
cd face-blur-magic/backend
```

### 2. Create and activate a virtual environment

```bash
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the FastAPI server

```bash
uvicorn main:app --reload
```

Your backend will be running at `http://127.0.0.1:8000`

---

## 📦 `requirements.txt`

Below is a typical list of required packages (add more if used):

```
fastapi
uvicorn
opencv-python
retina-face
python-multipart
```

Save the above in `backend/requirements.txt`.

---

## 🖼️ Frontend Setup

Just open the file in your browser:

```bash
cd ../frontend
open index.html   # or just double click to open it
```

To connect the frontend to a **local backend**, change this line in the `<script>`:

```js
const response = await fetch('http://127.0.0.1:8000/process', {
  method: 'POST',
  body: formData
});
```

---

## 📤 API Reference

### POST `/process`

Upload an image and receive the processed image with blurred faces.

- **Method**: `POST`
- **Body**: `multipart/form-data` (with field named `file`)
- **Response**: JPEG (`image/jpeg`)

### Example in JavaScript:

```js
const formData = new FormData();
formData.append('file', yourFile);

const response = await fetch('/process', {
  method: 'POST',
  body: formData
});

const blob = await response.blob();
const imageUrl = URL.createObjectURL(blob);
```

---

## 🔧 Sample `main.py` (Backend logic)

```python
import cv2 as cv
import numpy as np
from retinaface import RetinaFace
from fastapi import FastAPI, UploadFile, File
from fastapi.responses import Response
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["*"],
    allow_headers=["*"],
)

@app.post("/process")
async def process(file: UploadFile = File(...)):
    contents = await file.read()
    np_arr = np.frombuffer(contents, np.uint8)
    img = cv.imdecode(np_arr, cv.IMREAD_COLOR)

    faces = RetinaFace.detect_faces(img)
    if isinstance(faces, dict):
        for key, value in faces.items():
            x1, y1, x2, y2 = value["facial_area"]
            roi = img[y1:y2, x1:x2]
            blurred = cv.GaussianBlur(roi, (15, 15), 0)
            img[y1:y2, x1:x2] = blurred

    _, buffer = cv.imencode(".jpg", img)
    return Response(content=buffer.tobytes(), media_type="image/jpeg")
```

---

## 🤝 Contributing

We welcome contributions! Here’s how you can help:

1. Fork the repo
2. Create your feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m 'Add your message'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Create a new Pull Request

---

## 📃 License

This project is open source under the [MIT License](LICENSE).

---

## 🙋‍♂️ Author

Made with ❤️ by [@krrishcoder07](https://github.com/krrishcoder07)
