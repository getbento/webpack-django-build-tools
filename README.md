# Webpack Django Build Tools
A set of postbuild tools for ensuring Webpack built JavaScript applications work seemlessly with Django

# 1 Update ```index.html``` With Static Tags

## 1.1 Summary
To make use of Django and friends handling of static files with their unique hashes we need to replace hard links the JavaScript application bundle, maps, and other static files with their associated static template tag.

## 1.2 Implementation Steps
### 1.2 Step 1: Copy ```static_tag.js``` to Project Directory
From this GitHub directory clone and copy the util's folder into your project's root directory. An example project directory is below:
```
<app_name>
├── README.md
├── dist
├── node_modules
├── package-lock.json
├── package.json
├── src
├── utils/
    ├── static_tag.js
├── webpack.config.babel.js
└── yarn.lock
```

### 1.2 Step 2: Update ```package.json```
For this step in the ```package.json``` script section we will update the build line from:
```
"build": "webpack -p --progress"
```
to:
```
"build": "webpack -p --progress && node utils/static_tag.js <app_name>"
```
This will run a second command after the bundle build process that updates the ```index.html```.

### 1.2 Step 3: Run ```yarn build```
Now when yarn build is run, the ```index.html``` will be updated and the JavaScript bundle and favicon path's will be updated with template tags that the Django or Jinja2 template language can read.