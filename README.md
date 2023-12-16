# streamlit-bokeh3-events
A streamlit component for bi-directional communication with bokeh 3 plots. This update is based on the following archived repository from ash2shukla: https://github.com/ash2shukla/streamlit-bokeh-events

# General remarks
The original implementation of ash2shukla looks very promising, however, I was not able to get it running on my system. Moreover, it does not support bokeh3 and is not maintained anymore. For this repository, I took the code from ash2shukla and updated it to work with bokeh3. My plan is to generate a pip package and add it as a streamlit component. I am not quite there, so if you are experienced with JS, please read further.

# Installation
- Install all requirements listed [here](https://docs.streamlit.io/library/components/components-api#development-environment-setup)
- clone this repository
- navigate to `streamlit_bokeh3_events/frontend`
- run `npm install`
- run `npm run start`
- open another terminal and navigate to the directory where you cloned the repo
- run `pip install .`
- execute `streamlit run example/example.py`  
Your browser will now show a nice streamlit app where you can interactively select data points from a bokeh plot using a lasso tool. I also tested all other examples from ash2shukla and they worked.

# Packaging
To get a pip package, we have to build the frontend, which can be achieved by running `npm run build` in the frontend directory. This produces a production build that can be later digested by pip. On my system it builds successfully. You can now use the build to run the server (just as before with `npm run start`) using the following command: `serve -s build -l 3001`. (Remark: maybe you have to install serve before by using `npm install -g serve`).  
On my system, this gives an error that you can see in your browser by inspection (e.g. F12 in Chrome):
```
Uncaught TypeError: M is not a constructor
    O http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    8353 http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    __webpack_require__ http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    1678 http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    __webpack_require__ http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    553 http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    __webpack_require__ http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    16 http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    __webpack_require__ http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    3731 http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    __webpack_require__ http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    3285 http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    __webpack_require__ http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    <anonymous> http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    <anonymous> http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
    <anonymous> http://192.168.2.40:3001/static/js/main.e00fee0f.js:2
```
Due to this error, the streamlit app cannot run properly and it complains 
```
(The app is attempting to load the component from http://localhost:3001, and hasn't received its "streamlit
" message.)
```  
These are my installed versions:  
```
npm -v
10.2.4
node -v
v21.3.0
```  
In short: the component already runs successfully with the frontend part in development mode (using ```npm run start```) and fails in optimized mode (using ```npm run build```).  
**If anyone can help me with this [issue](https://github.com/ChristophNa/streamlit-bokeh3-events/issues/1) we can make an updated version of ash2shukla's repository with the newest bokeh version. Even testing and trying to reproduce the error on other systems would already help.**
