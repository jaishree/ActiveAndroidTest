You will need to attach an Android device via USB or create an emulator in order to run the test suite. We'll describe how to create and run an emulator below but skip those sections if you have a device attached.

### Create an Emulator Profile

First, create an emulator profile (if you do not already have one) by going to your `sdk/tools` directory and entering:

    ./android avd

This will launch the AVD Manager and allow you to create a device emulator for running the tests. You can create anything fairly standard here that you want, or use one that you already have setup.


### Run Emulator

Either start the emulator from the AVD Manager or from the command line in the `sdk/tools` directory with:

    ./emulator -avd YourEmulatorName


### Run the Test Suite

Go to the ActiveAndroid root directory and run the test suite with the following command:

    mvn clean install

The test suite should run and output a successful build result similar to the following:

    [INFO] ------------------------------------------------------------------------
    [INFO] Reactor Summary:
    [INFO] 
    [INFO] ActiveAndroid - Parent ............................ SUCCESS [0.351s]
    [INFO] ActiveAndroid ..................................... SUCCESS [3.880s]
    [INFO] ActiveAndroid - Tests ............................. SUCCESS [36.252s]
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time: 42.173s
    [INFO] Finished at: Sun Mar 02 12:22:37 MST 2014
    [INFO] Final Memory: 18M/81M
    [INFO] ------------------------------------------------------------------------


### Issues and Updates

If you have any trouble with this, send [Josh](https://github.com/joshuapinter) or [Sean](https://github.com/SeanPONeil) a message.

Also, if you had to complete any additional steps to successfully run the test suite, please update this Wiki with what you did for the benefit of others.
