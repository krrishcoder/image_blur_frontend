# 🔐 Face Blur Magic

Protect your privacy with AI-powered face detection and blurring.  
This project provides a beautifully animated **frontend interface** where users can upload an image and view **Before/After** results.

---

## 🌐 Live Demo

- 🔗 Frontend: [https://krrishcoder.github.io/image_blur_frontend/](https://krrishcoder.github.io/image_blur_frontend/)
- 🧠 API Endpoint (backend): [https://krrishcoder07-face-blur-app.hf.space/process](https://krrishcoder07-face-blur-app.hf.space/process)

---

## 🗂 Project Structure

```
image_blur_frontend/
├── index.html         # Main HTML UI
├── style.css          # CSS styling and animations
├── README.md          # Project documentation
```

---

## 🌟 Features

- 📸 Upload any image
- 🧠 AI detects faces and blurs them
- 🎨 Beautiful before/after comparison
- ✨ Animated, responsive UI
- 💻 Uses public backend hosted on HuggingFace Spaces

---

## 🧠 Tech Stack

- **Frontend**: HTML, CSS, JavaScript
- **Backend (hosted)**: FastAPI, RetinaFace, OpenCV (not included in this repo)
- **Deployment**: GitHub Pages + Hugging Face Spaces

---

## 💡 How to Use

1. Open the app in your browser:  
   👉 [https://krrishcoder.github.io/image_blur_frontend/](https://krrishcoder.github.io/image_blur_frontend/)

2. Click **"Choose Image File"** and select a photo with faces

3. Hit the **"✨ Process Image"** button

4. View the **Before** and **After** results!

---

## 📤 API Reference (Used Behind the Scenes)

**Endpoint:** `POST https://krrishcoder07-face-blur-app.hf.space/process`  
**Payload:** `multipart/form-data` with a `file` field (image)

### JavaScript Upload Sample

```js
const formData = new FormData();
formData.append('file', fileInput.files[0]);

const response = await fetch('https://krrishcoder07-face-blur-app.hf.space/process', {
    method: 'POST',
    body: formData
});

const blob = await response.blob();
const imageUrl = URL.createObjectURL(blob);
document.getElementById('outputImage').src = imageUrl;
```

---

## 🤝 Contributing

We welcome contributions! Here's how to get started:

1. **Fork** the repository  
2. **Clone** your fork  
   ```bash
   git clone https://github.com/your-username/image_blur_frontend.git
   ```
3. Create a new branch  
   ```bash
   git checkout -b feature/your-feature
   ```
4. Make your changes and commit  
   ```bash
   git commit -m "Add your feature"
   ```
5. Push your branch and create a Pull Request  

---

## 📃 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙋‍♂️ Author

Made with ❤️ by [@krrishcoder07](https://github.com/krrishcoder07)
