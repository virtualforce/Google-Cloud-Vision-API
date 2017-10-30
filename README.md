# Google-Cloud-Vision-API
Google Cloud Vision API enables developers to understand the content of an image by encapsulating powerful machine learning models in an easy to use REST API. It quickly classifies images into thousands of categories (e.g., "sailboat", "lion", "Eiffel Tower"), detects individual objects and faces within images, and finds and reads printed words contained within images.

## Getting Started
The Vision API consists of a single endpoint (https://vision.googleapis.com/v1/images) that supports one HTTP request method (annotate):
POST https://vision.googleapis.com/v1/images:annotate

For now, we will enque only two features here to show how its work:
1. Text Detection (OCR)   
2. Label Detection

## 1. Text Detection (OCR)
The Vision API can detect and extract text from images. here we are discussing only one feature that support OCR:

1.1 TEXT_DETECTION   
1.2 DOCUMENT_TEXT_DETECTION

### 1.1 TEXT_DETECTION
It detects and extracts text from any image. For example, a photograph might contain a street sign or traffic sign. The JSON includes the entire extracted string, as well as individual words, and their bounding boxes.

#### How its work?
The body of your POST request contains a JSON object of type AnnotateImageRequest, such as:

```
{
  "image": {
    object(Image)
  },
  "features": [
    {
      object(Feature)
    }
  ],
  "imageContext": {
    object(ImageContext)
  },
}
```

#### Sample Request
Image can be sent as a base64-encoded string, a Google Cloud Storage file location, or as a publicly-accessible URL, ImageContext is optional & used very rarely based on your request parameters, So we are skipping it. You can try this request in Google Vision API [console] (https://developers.google.com/apis-explorer/?hl=en_GB#p/vision/v1/) window:

```
{
  "requests": [
    {
      "image": {
        "content": "/9j/7QBEUGhvdG9zaG9...base64-encoded-image-content...fXNWzvDEeYxxxzj/Coa6Bax//Z"
      },
      "features": [
        {
          "type": "TEXT_DETECTION"
        }
      ]
    }
  ]
}
```


### 1.2 DOCUMENT_TEXT_DETECTION
It also extracts text from an image, but the response is optimized for dense text and documents. The JSON includes page, block, paragraph, word, and break information.
