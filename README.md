
# Vue Midterm Project

## Setting Up the Project Folder

1. **Create a New Folder**  
   Start by making a new folder for your project. Open the terminal in that folder by holding the `Shift` key and right-clicking on the folder.

   ![Opening terminal in folder](https://i.imgur.com/SRZJOgZ.gif)

## Installing the Vue CLI

2. **Set Up the Vue Environment**  
   In the terminal, run the following command to install the Vue CLI globally:

   ```sh
   npm i -g @vue/cli-init 
   ```

3. **Initialize the Vue Project**  
   Now, initialize the Vue project by running the command below:

   ```sh
   vue init webpack vue-midterm
   ```

4. **Installing Dependencies**  
   During the setup, you might be prompted to install some dependencies. Type `Y` and press `Enter` to continue.

   ![Installing dependencies](https://i.imgur.com/GxyPomD.png)

## Running the Vue Project

5. **Navigate to the Project Folder**  
   Once the initialization is complete, enter the project directory and install the required packages by running the following commands:

   ```sh
   cd vue-midterm
   npm install
   npm run dev
   ```

6. **Open the Project in the Browser**  
   After running these commands, the terminal should display a link. Open that link in your browser by holding the `Ctrl` key and clicking on it.

   ![Opening project link](https://i.imgur.com/enOigyr.png)

## Verifying the Setup

7. **Check the Vue Setup**  
   If everything is working correctly, you should see the following screen in your browser:

   ![Vue setup confirmation](https://i.imgur.com/qQ15hGL.png)

## Vue Midterm Project Code

8. **Creating a Nav Bar**  
   This can be done by editing the `App.vue` file in the `src` folder and the `index.js` file in the `router` folder.

   ![App.vue file](https://i.imgur.com/PdCYaet.png)
   ![index.js file](https://i.imgur.com/MyuQYX4.png)

   With this, you should be able to see the navigation bar on the browser and have it navigate to the different pages when it is pressed.

9. **Turning on Your RapidAPI Key and Making Sure It Is Working**  
   Visit the RapidAPI website and turn on the key you want to use. In our use case, we used the WeatherAPI.com API key.

   [WeatherAPI.com on RapidAPI](https://rapidapi.com/weatherapi/api/weatherapi-com)

   ![WeatherAPI.com](https://i.imgur.com/aRZY3Nk.png)

   Make sure you log in (you will have to sign up if you don't have an account) and turn on the key. You can then use the key in your project.

   ![WeatherAPI.com key activation](https://i.imgur.com/dHV3OMW.gif)

   **If this is not done, your API key will not work. This is very important. Make sure it is done.**

10. **Creating a Weather Component**  
    This was done by editing the `FormView.vue` file in the `views` folder and the `Weather.vue` file in the `components` folder.

    Depending on the requirements, all you have to do is edit that file; there is no reason to touch any other file.

    **USE ChatGPT** if you need help or get stuck.
