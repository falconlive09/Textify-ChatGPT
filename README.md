# Textify ChatGPT

# Notes Regarding Code: 
- The content.js file is the content script that has all of the actual logic of the extension in terms of loading and initializing the tesseract worker, injecting the buttons and other UI elements into the ChatGPT page, etc. 
- The popup.js file connects to the popup.html for configuring the options and saving it to the chrome local storage for the content.js to later retrieve. 
- The tesseract.min.js file is from Tesseract.js and contains all the code related to the Tesseract engine itself. 
- As noted in their API, the [Worker.loadLanguage(langs, jobId): Promise
]([url](https://github.com/naptha/tesseract.js/blob/master/docs/api.md#worker-load-language)) method fetches the trainedData files from their CDNs if its not already in cache and saves it into Chrome's IndexedDB storage. This makes it convienient for users loading languages, but it also means featching and downloading it can take a while for some languages. 
- The content.js and tesseract.min.js file are specified as content scripts in the manifest v3 file and get auto injected on page refesh by chrome. 

# Important Note due to CSP Restrictions and Regarding Language Support 
The ChatGPT website finally added CSP restrictions (August 2023) which block fetching language files from Tesseract.js CDNs. What this means is that the 100+ languages there were able to be picked and downloaded on a need basis is no longer easily possible. As a compromise, I picked out a dozen languages that have had the most use and engangement and they now are packed inside the extension, it should cover for more than 95% of usecases. 

In addition, I also bundled the worker and core files since they also can no longer be fetched from the CDN at runtime. This means that the total size of the extension has comparatively greatly increased. Fortunately, other than a slower initial download size of the actual extension, performance should remain the same and the extension still works as before. 

Version 0.0.0.7 was the last version with CDN fetching, it is saved on a separate branch or can be referenced through the commit history for anyone that would like to reference that code. It should still work as long as the target website does not have CSP policies blocking external scripts. 

Version 0.0.0.8 and on will bundle the necessary files for the extension to run appropriately. 


# Product-Description
Update: Supports 10+ Major Languages! 

This extension was born out of a need for a fast, quick and intuitive way to get text from images into the textbox for ChatGPT. This extension accomplishes this with a great degree of accuracy and average speeds of ~5 seconds or less. 

Now, you don't have to switch between multiple tools just for Optical Character Recognition (OCR). With this extension, you can easily upload an image file or drag and drop it for conversion into text, which will automatically populate your ChatGPT textbox. 

Additionally, if you have a screenshot in your clipboard, you can directly paste (Ctrl+V) it into the textbox. Quick, hassle-free, and highly efficient - this extension is built with a focus on speed, user-friendliness, and most importantly, privacy.

For the Tech Savvy:
Powered by Tesseract.js, this extension runs OCR directly in your browser, keeping your data secure as none of your information leaves your device. All the OCR work is performed locally, ensuring maximum privacy.

But we understand that sometimes, you may need an extra level of precision or need to retain the original format of the image, especially when dealing with content like Python code. For such instances, we provide an option to enable an embedded third-party solution created by Pieces.app. Check out their service at: https://www.codefromscreenshot.com/

Disclaimer: Please note, if you opt to use the third-party embedded option, your privacy and data handling will be subject to their policy as this extension is not affiliated with them.
