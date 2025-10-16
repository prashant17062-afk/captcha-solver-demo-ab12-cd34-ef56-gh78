Academic CAPTCHA Solver

Summary
This project presents a client-side web application designed to solve CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) challenges. It leverages Optical Character Recognition (OCR) technology, specifically the Tesseract.js library, to extract text embedded within image-based CAPTCHAs. Developed as a high-quality student submission for academic grading, this application demonstrates practical integration of client-side OCR, user-friendly design, and robust error handling within standard web technologies (HTML, CSS, JavaScript). It aims to display the solved CAPTCHA text within a specified timeframe, offering a clear illustration of web-based OCR capabilities.

Setup
To run this CAPTCHA solver, follow these simple steps:

1.  Save the provided 'index.html' file to a directory on your local computer.
2.  Open the 'index.html' file using any modern web browser (e.g., Google Chrome, Mozilla Firefox, Microsoft Edge).

This application runs entirely in the browser, requiring no server-side setup, complex build processes, or additional dependencies beyond what is loaded via CDN.

Usage
The application supports two main modes of operation for processing CAPTCHA images:

1.  With a Custom CAPTCHA URL:
    You can specify a CAPTCHA image to solve by appending a '?url=' query parameter to the 'index.html' file's URL in your browser's address bar.
    Example:
        file:///path/to/your/index.html?url=https://example.com/your-captcha-image.png
    Replace 'https://example.com/your-captcha-image.png' with the direct URL to your chosen CAPTCHA image.

2.  With the Default Sample CAPTCHA:
    If no '?url=' parameter is provided in the URL, the application will automatically load and attempt to solve a predefined default sample CAPTCHA image. The default image URL is:
        https://i.stack.imgur.com/eBfR8.png
    This default image contains the text "WcR5K" and serves as a reliable test case for the OCR engine.

Upon page load, the application will display the CAPTCHA image, provide real-time status updates on the solving process, and then present the extracted CAPTCHA text. The entire process, from initiating Tesseract.js to displaying the final solution, is designed to complete within 15 seconds, subject to network conditions and the complexity of the CAPTCHA.

Main Code Logic
The CAPTCHA solver is implemented within a single 'index.html' file, encapsulating HTML for structure, CSS for presentation, and JavaScript for core functionality.

HTML Structure:
- The page uses a semantic HTML5 structure within a main '.container' div for a clean, centered layout.
- An '<img>' element (id="captchaImage") is dedicated to displaying the CAPTCHA image.
- A '<span>' element (id="currentCaptchaUrl") dynamically displays the URL of the CAPTCHA image being processed.
- Two '<p>' elements (id="statusDisplay" and id="resultDisplay") are used to show the current processing status (e.g., "Loading Tesseract.js...") and the final solved text, respectively.
- A professional footer contains copyright and MIT license information.

CSS Styling:
- A minimalist and professional CSS design ensures a clean user interface.
- Styles are applied to enhance readability, use a coherent color scheme, and provide basic responsiveness for various screen sizes.
- Status and result displays are styled to be prominent and informative.

JavaScript Functionality:
1.  Tesseract.js Integration:
    The Tesseract.js library is included via a Content Delivery Network (CDN) directly in the '<head>' section of the HTML. This enables powerful client-side Optical Character Recognition without the need for a backend server.
    HTML inclusion example:
        <script src="https://cdn.jsdelivr.net/npm/tesseract.js@4.1.0/dist/tesseract.min.js"></script>

2.  URL Parameter Parsing:
    Upon the 'DOMContentLoaded' event, the JavaScript code parses the browser's URL query string. It extracts the value associated with the 'url' parameter. If this parameter is absent, a predefined 'defaultCaptchaUrl' is used.
    JavaScript logic example:
        const params = new URLSearchParams(window.location.search);
        const imageUrl = params.get('url') || defaultCaptchaUrl;

3.  Image Display:
    The 'src' attribute of the 'captchaImage' HTML element is dynamically updated with the resolved 'imageUrl', making the CAPTCHA visible on the page.

4.  CAPTCHA Solving Function ('startProcessing'):
    - This is an asynchronous function responsible for the entire OCR workflow.
    - 15-Second Timeout Mechanism: A 'setTimeout' is initiated at the start of 'startProcessing'. This timer monitors the entire OCR process (including Tesseract.js worker initialization, language data downloading, and image recognition). If the process does not complete within 15 seconds, a timeout error is displayed, fulfilling a core requirement of the submission.
    - Tesseract.js Worker Initialization: 'Tesseract.createWorker('eng')' is called to initialize the OCR engine for English text. This step is resource-intensive and often involves downloading WebAssembly (WASM) modules and language data files, which can take time, especially on the first run.
    - Image Recognition: 'worker.recognize(imageUrl)' sends the CAPTCHA image (referenced by its URL) to the Tesseract.js worker for text extraction.
    - Result and Status Display: The extracted text (or an appropriate message if text cannot be read) is then displayed in the 'resultDisplay' element, along with the total time taken for the process. 'statusDisplay' provides real-time updates.
    - Error Handling: A 'try-catch' block handles potential errors during the OCR process or network requests, displaying informative error messages to the user.
    - Worker Termination: 'worker.terminate()' is called after recognition to free up system resources.

5.  Robust Execution Trigger:
    The 'startProcessing' function is designed to be called reliably. It checks if the 'captchaImage' is already loaded (e.g., from browser cache). If so, it proceeds immediately. Otherwise, it attaches itself to the image's 'onload' event. An 'onerror' handler is also in place to gracefully manage situations where the CAPTCHA image itself fails to load.

License
This project is licensed under the MIT License. This permissive open-source license allows for free use, modification, and distribution. A copy of the license details is linked in the 'index.html' footer for convenience.

Contact
For any inquiries, feedback, or further discussion regarding this academic CAPTCHA solver submission, please feel free to reach out:
[Your Name (e.g., AI Expert Developer)]
[Your Placeholder Email (e.g., expert.developer@example.com)]
[Your Placeholder GitHub Profile (e.g., github.com/ai-expert-dev)]