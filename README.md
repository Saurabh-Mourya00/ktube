🏋️‍♂️ YouTube Fitness Community Post Automation
An automated backend service built with FastAPI and Python (Pillow) that processes fitness background images, applies professional motivational quote overlays, publishes them to YouTube, and automatically deletes temporary files to save server storage.

🚀 Features
FastAPI Backend: High-performance async API endpoints for fast file handling.

Dynamic Image Processing: Automatically resizes, wraps text, adds high-contrast dark text-boxes, and positions quotes (top, middle, bottom) onto multiple images at once.

Automated Storage Cleanup: Self-destructs raw uploads and processed image files from the server immediately after posting to save storage space.

YouTube API Integration: Seamlessly handles multi-image posting workflows.

📁 Project Structure
Plaintext
youtube-fitness-automation/
│
├── temp_images/          # Temporary storage for raw and processed images (auto-cleaned)
├── main.py               # FastAPI application entry point
├── requirements.txt      # Python dependencies
└── README.md             # Project documentation
🛠️ Installation & Setup
1. Clone the Repository & Setup Virtual Environment
Bash
git clone <your-repository-url>
cd youtube-fitness-automation
python -m venv venv
2. Activate Virtual Environment
Windows (CMD/PowerShell):

DOS
venv\Scripts\activate
Mac / Linux:

Bash
source venv/bin/activate
3. Install Dependencies
Bash
pip install fastapi uvicorn pillow python-multipart requests
⚙️ Running the Server
Start the development server using Uvicorn:

Bash
uvicorn main:app --reload --port 8000
Once running, access the interactive API documentation (Swagger UI) at:
👉 http://localhost:8000/docs

🔌 API Usage (POST /create-post/)
You can test the endpoint directly via the Swagger UI or using curl:

Endpoint: /create-post/

Method: POST

Form Parameters:

quote: The motivational text to overlay (e.g., "Push past your limits!")

position: Text placement choice (top, middle, bottom)

images: Multiple image files (.jpg, .png) up to 5 images.

🧹 Storage Self-Destruct Mechanism
The application utilizes FastAPI's BackgroundTasks. As soon as the images are processed and published:

The script dispatches the post payload.

Upon success, it loops through the local /temp_images/ directory.

Every raw input image and rendered output file is permanently deleted (os.remove()), ensuring your server storage never fills up.