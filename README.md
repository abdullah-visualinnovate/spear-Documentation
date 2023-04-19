# Spear Application

A Spear project created in flutter using BLOC. Spear supports both Android and Ios, clone the appropriate branches mentioned .


## Getting Started

The application consists of three applications, the first is for the user, and through it he adds the accident that occurred to his car, then the request goes to Rum Company, which is a private insurance company. The rum company agrees to the offers, and then comes the last part of the garage application, which enables the garage owner to receive requests from the sellers and submit a report on the status of each piece to the rum company

## How to Use

### Step 1:

Download or clone this repo

Step 2:

Go to project root and execute the following command in console to get the required dependencies

```
flutter pub get 
```
Step 3:

This project uses Prepare library:

```
flutter channel stable
flutter upgrade
```

run app:

```
flutter run
```

## Spear User Feature

1.	Register Screen with validation
2.	Login Screen with validation
3.	Forget Password
4.	Add Accedience
5.	History of 
6.	Profile
7.	Edit Profile 
8.	Support Screen
9.	Splash Screen
10.	logout

## Spear Vendor Feature

1.	Splash
2.	Register with validation
3.	Login with validation
4.	Forget Password
5.	Profile
6.	Edit Profile
7.	Support
8.	Order List
9.	Order Details
10.	Garage Profile Screen
11.	Submit Offer Screens (New , used , Muiltuple)
12.	Offer List Screen (pending , Accepted)
13.	Offer Details Screen
14.	Chat List Screen
15.	Chat Details Screen
16.	Notification


## Spear Garage Feature

1.	Splash
2.	Register with validation
3.	Login with validation
4.	Forget Password
5.	Profile
6.	Edit Profile
7.	Support
8.	Garage List
9.	Garage Details
10.	Accept Pieces
11.	Not Accept Pieces
12.	Chat List Screen
13.	Chat Details Screen


## Libraries & Tools Used

1.	flutter_bloc
2.	dio
3.	file_picker
4.	record
5.	path_provider
6.	carsouel_slider
7.	flappy_search_bar
8.	flatter_math_fork
9.	mdi
10.	image_picker
11.	smooth_page_indicator
12.	flutter_lancher_icons
13.	lottie
14.	http
15.	share_preferences
16.	url_lancher
17.	material_design_icons_flutter


## Folder Structure

Here is the core folder structure which flutter provides.

```

flutter-app/
|- android
|- build
|- ios
|- lib
|- test

```

Here is the folder structure we have been using in this project

```
lib/
|- constants/
|- data_layer/
|- business_logic_layer/
|- presentation_layer/
|- widgets/
|- main.dart
|- routes.dart

```


Now, lets dive into the lib folder which has the main code for the application.

```
1- constants - All the application level constants are defined in this directory with-in their respective files. This directory contains the constants for `theme`, `dimentions`, `api endpoints`, `preferences` and `strings`.
2- data_layer - Contains the data layer of your project, includes directories for local, network and shared pref/cache.
3- business_logic_layer - Contains store(s) for state-management of your application, to connect the reactive data of your application with the UI. 
4- presentation_layer — Contains all the ui of your project, contains sub directory for each screen.
5- widgets — Contains the common widgets for your applications. For example, Button, TextField etc.
6- routes.dart — This file contains all the routes for your application.
7- main.dart - This is the starting point of the application. All the application level configurations are defined in this file i.e, theme, routes, title, orientation etc.
```


## Constants
This directory contains all the application level constants. A separate file is created for each type as shown in example below:

```
constants/
|- my_colors
|- strings.dart
```

## Data

All the business logic of your application will go into this directory, it represents the data layer of your application. It is sub-divided into three directories local, network and sharedperf, each containing the domain specific logic. Since each layer exists independently, that makes it easier to unit test. The communication between UI and data layer is handled by using central repository.

```
data_layer/
|- model/
    |- order_list_model.dart
    |- order_details_model.dart
    |- offer_list_model.dart
    |- offer_details_model.dart
    |- my_profile_model.dart
    |- chat_list_model.dart
   
|- repository/
   
    |- user_repository.dart
    
|- web_services
    |- user_web_services.dart
    
|- repository.dart

```

## business_logic_layer

The store is where all your application state lives in flutter. The Store is basically a widget that stands at the top of the widget tree and passes it's data down using special methods. In-case of multiple stores, a separate folder for each store is created as shown in the example below:

```
business_logic_layer/
|- cubit/
    |- user_cubit.dart
    |- user_state.dart

```

## presentation_layer

This directory contains all the ui of your application. Each screen is located in a separate folder making it easy to combine group of files related to that particular screen. All the screen specific widgets will be placed in widgets directory as shown in the example below:

```
/presentation layer
|- screen
|- widgets
      
```

## Widgets

Contains the common widgets that are shared across multiple screens. For example, Button, TextField etc.

```
widgets/
|- custom_text_field.dart
|- custom_password_field.dart
|- custom_multi_select_drop_down.dart

```

## Routes

This file contains all the routes for your application.

```
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

class AppRouter {

  late UserCubit userCubit;
  late UserRepository userRepository;
  AppRouter(){

    userRepository = UserRepository(UserWebServices());
    userCubit = UserCubit(userRepository);
  }

  Route? generateRoute(RouteSettings settings) {
    switch (settings.name) {


    
     case splashScreen:
        return MaterialPageRoute(
          builder: (_) => BlocProvider(
              create: (BuildContext context) => userCubit,
              child: SplashScreen()
          ),
        );
        


      case registerScreen:
        return MaterialPageRoute(
          builder: (_) => BlocProvider(
              create: (BuildContext context) => userCubit,
              child:  Register()
          ),
        );

      case loginScreen:
        return MaterialPageRoute(
          builder: (_) => BlocProvider(
              create: (BuildContext context) => userCubit,
              child:   Login()
          ),
        );


      case homeScreen:
         return MaterialPageRoute(
          builder: (_) => MultiBlocProvider(
            providers: [
              BlocProvider<UserCubit>(create: (_) => UserCubit(userRepository)),
              BlocProvider<OrderCubit>(create: (_) => OrderCubit(userRepository)),
              BlocProvider<OffersCubit>(create: (_) =>                OffersCubit(userRepository)),
              BlocProvider<ChatCubit>(create: (_) => ChatCubit(userRepository)),
            ],

            child:  const Home(),
          ),
        );

      case orderDetailsScreen(int id):
        return MaterialPageRoute(
          builder: (_) => BlocProvider(
              create: (BuildContext context) => userCubit,
              child:   ProjectDetails()
          ),
        );

      case settingScreen:
        return MaterialPageRoute(
          builder: (_) => BlocProvider(
              create: (BuildContext context) => userCubit,
              child:   Setting()
          ),
        );


      case forgetPasswordScreen:
        return MaterialPageRoute(
          builder: (_) => BlocProvider(
              create: (BuildContext context) => userCubit,
              child:   ForgetPassword()
          ),
        );



    }
  }
}
```


## main

This is the starting point of the application. All the application level configurations are defined in this file i.e, theme, routes, title, orientation etc

```

import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart';
import 'package:flutter/services.dart';



void main(){

  WidgetsFlutterBinding.ensureInitialized();
  SystemChrome.setPreferredOrientations([
    DeviceOrientation.portraitUp,
    DeviceOrientation.portraitDown,
  ]);
  runApp(
      MyApp(
    appRouter: AppRouter(),
  ));
}


class MyApp extends StatelessWidget {


  final AppRouter appRouter;

  const MyApp({super.key, required this.appRouter});

  @override
  Widget build(BuildContext context) {

    ErrorWidget.builder = (FlutterErrorDetails details) {
      return Material(
        child: Container(
          color: MyColors.colorOverlay,
          alignment: Alignment.center,
          child: const Text(
            'Something went wrong! Check your Network Access',
            style: TextStyle(fontSize: 20, color: Colors.white),
          ),
        ),
      );
    };

    return MaterialApp(
      onGenerateRoute: appRouter.generateRoute,
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
          textTheme: GoogleFonts.robotoTextTheme()
      ),
      title: "Spear",
    );
  }
}

```
