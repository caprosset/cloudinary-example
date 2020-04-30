# cloudinary-example

### Install packages

```
npm install cloudinary multer-storage-cloudinary multer --save
```

### In config folder new file cloudinary.js

```
const cloudinary = require('cloudinary');
const cloudinaryStorage = require('multer-storage-cloudinary');
const multer = require('multer');
require('dotenv').config();
 
cloudinary.config({
  cloud_name: process.env.CLOUDINARY_CLOUD_NAME,
  api_key: process.env.CLOUDINARY_API_KEY,
  api_secret: process.env.CLOUDINARY_API_SECRET
});

const storage = cloudinaryStorage({
  cloudinary: cloudinary,
  folder: 'name folder',
  allowedFormats: ['jpg', 'png', 'jpeg', 'gif']
});
 
const parser = multer({ storage: storage });

module.exports = parser
```


### In the hbs view

```
<form action="/your-endpoint" method="POST" enctype="multipart/form-data">
  <input type="file" name="photo" />
  <button type="submit">New GIF</button>
</form>
```


### In the router where we want to upload the image

```
const parser = require('./../config/cloudinary');

router.post('/your-endpoint', parser.single('photo'), (req, res, next) =>{
 
 const image_url = req.file.secure_url
 
}
```
