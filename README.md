# Textify ChatGPT

# Notes Regarding Code: 
- The content script, or content.js file, contains all of the code necessary to load and initialize the Tesseract worker, inject buttons and other user interface components into the ChatGPT page, and other tasks. 
- To configure the settings, the popup.js file connects to the popup.html and saves it to the Chrome local storage, which the content.js file will subsequently access. 
- All of the code for the Tesseract engine itself is included in the tesseract.min.js file, which is a subdirectory of Tesseract.js. 
- The [Worker.loadLanguage(langs, jobId): Promise] is mentioned in their API.If the trainedData files aren't already in cache, the ([url](https://github.com/naptha/tesseract.js/blob/master/docs/api.md#worker-load-language)) function retrieves them from respective CDNs and stores them in Chrome's IndexedDB storage. Users will find it convenient as a result to load languages, however featching and for certain languages, the download process may take some time. 
- The manifest v3 file specifies the content scripts content.js and tesseract.min.js, which are automatically injected by Chrome on page refresh. 

# Important Note due to CSP Restrictions and Regarding Language Support 
In August 2023, the ChatGPT website finally implemented CSP constraints that prevent language files from Tesseract.js CDNs from being fetched. This implies that it is no longer simple to select and download any of the more than 100 languages as needed. In an attempt to reach a compromise, I selected twelve languages that have had the highest usage and engagement; they are now included in the extension, which should cover over 95% of use cases. 

Since the worker and core files can no longer be retrieved from the CDN at runtime, I have also packaged them. This indicates that the extension's overall size has significantly risen. Thankfully, aside from the fact that the extension's first download took longer than expected, performance should remain the same and the extension still works as before.

# Product-Description
Update: Supports 10+ Major Languages! 

The desire for a simple, quick, and speedy method of transferring text from photos into the ChatGPT textbox gave rise to this addon. This extension achieves average speeds of less than 5 seconds and a high degree of precision. 

You may now use one tool for optical character recognition (OCR) instead of switching between numerous ones. This extension makes it simple to upload or drag and drop picture files to convert them to text, which will then automatically fill your ChatGPT textbox. 

Moreover, you may paste (Ctrl+V) a screenshot that is in your clipboard straight into the textbox. This extension is designed to be quick, easy to use, and extremely effective. It prioritizes speed, user-friendliness, and most importantly, privacy.

# For the Tech Enthusiast
This extension, which uses Tesseract.js to power it, does OCR from within your browser, protecting your data because it never leaves your device. Since all OCR work is done locally, the highest level of privacy is guaranteed.

However, we recognize that, on occasion, you could want an additional degree of accuracy or that you might need to keep the picture in its original format—particularly when working with information like Python code. In certain cases, we provide the ability to activate an integrated third-party solution made by Pieces.app. Visit https://www.codefromscreenshot.com/ to learn more about their offerings.

Disclaimer: Since this extension is not associated with the third-party, please be aware that your privacy and data handling will be subject to their policy if you choose to use the embedded option.
