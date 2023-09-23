# Bottom Camera Position

Now that we know the offset from the top camera to the nozzle, we can use the nozzle to set our bottom camera position.

!!! danger "Bottom Camera Z Position: v2 and v3 LumenPnP Differences"
    When inspecting the tip of the nozzle and parts that have been picked up, OpenPnP uses a saved Z height to bring the nozzle tip to so that it is in focus.

    Make sure your bottom camera Z position is set correctly based on your machine type and number of nozzles.

    v2 LumenPnP kits only have one tool head. The default Z-height is `61mm`. This is relatively high, and allows the bottom camera to see very large parts. But it is high enough that, if you have a second nozzle installed, the inactive nozzle can collide and cause damage.

    v3 semi-assembled LumenPnP machines come with two tool heads. To more safely accommodate this, the Z height is only `31.5mm`, and the bottom camera is mounted deeper below the Staging Plate. This ensures we can see large parts while preventing collisions with a second nozzle.

    * If you're using one nozzle, set the bottom camera Z Location to `61mm` (Standard for v2 LumenPnP kits).
    * If you're using two nozzles, set the bottom camera Z Location to `31.5mm` (Standard for v3 semi-assembled LumenPnP kits).

1. Click on the `Machine Setup` tab in the top right pane.
  ![Machine setup tab](images/Machine-Setup-Tab-3.png){ loading=lazy }

2. Click on the "Expand" checkbox to open all of the features about your machine.
  ![Expanding the Machine Config options](images/Expand-Checkbox-3.png){ loading=lazy }

3. Click on `Cameras > OpenPnpCaptureCamera Bottom`.
  ![Select the bottom camera](images/select-bottom-camera-2.png){ loading=lazy }

4. Click on the `Position` tab.
  ![Select the position tab](images/bottom-camera-position.png){ loading=lazy }

5. Set the camera's Z-axis location:
    * If you have a v2 LumenPnP **kit** with only one nozzle, set the Z axis value to `61mm`.
    * If you have a v3 **semi-assembled** LumenPnP with two nozzles, set the Z axis value to `31.5mm`.
  ![Set the z position](images/bottom-camera-z-pos.png){ loading=lazy }

6. Home your LumenPnP to make sure your toolhead's location is accurate. As before, ignore the `Nozzle tip calibration: not enough results from vision. Check pipeline and threshold` error if it appears.
  ![Home the machine](images/home-during-bottom-cam-pos.png){ loading=lazy }

7. Jog the toolhead off to the side so that it isn't aligned with any calibration points. This will make it easier to see if the nozzle is lined up with the bottom camera.
  ![Jog the toolhead](images/bottom-cam-jog-random.png){ loading=lazy }

8. Select the `Nozzle: N1 - N045 (Head:H1)` from the machine controls dropdown.
  ![Select nozzle from machine control dropdown](images/select-n1-machine-control-bottom.png){ loading=lazy }

9. Click the "Position tool over location" button to bring the left nozzle very roughly above the bottom camera.
  ![Position the toolhead over the bottom camera](images/position-over-bottom-cam.png){ loading=lazy }

10. Jog the toolhead until the left nozzle is directly in the center of the bottom camera's vision.
  ![Position the toolhead over the bottom camera precisely](images/position-over-bottom-cam-precise.png){ loading=lazy }

11. Click the "Capture Toolhead Location" button to calculate the correct position for the bottom camera.
  ![Store the camera location](images/store-nozzle-location-bottom.png){ loading=lazy }

12. Click the `Apply` button to save the new camera position.
  ![Save the camera location](images/apply-bottom-cam-pos.png){ loading=lazy }

## Next Steps

Next is [Nozzle Tip Calibration](../8-nozzle-tip-calibration/nozzle-tip-calibration.md).
