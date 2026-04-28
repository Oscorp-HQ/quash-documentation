# Local Emulators

To run tests on an emulator through Quash:

1. Install and run the emulator on your computer. To know about how to do it, [\[check this out\]](https://developer.android.com/studio/run/emulator).
2. Turn on USB debugging and wireless debugging from developer options.
3. In the Devices section on the Quash app, click on the "Scan for devices" button. You should see your emulator listed there.
4. Click on the "Connect" button next to the emulator. Your emulator will start showing under the connected devices section with device status as available.

> The Mahoraga Android App will automatically be installed on the emulator and will also have accessibility permissions automatically. If it does not happen, please do it manually once.
>
> In the Mahoraga app, make sure overlay is enabled and use the offset slider to correct the position of the bounding boxes and match it to your actual UI elements.&#x20;
>
> Once done, you can toggle off the overlay button.

You will now see the emulator listed as an option in the prompt box when you click on 'Devices', and can now run tasks on this emulator.

You can connect multiple devices to Quash and can run tests in parallel on them.
