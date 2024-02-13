---
title: "MM/pixel Calibration"
linkTitle: "MM/Pixel Calibration"
weight: 50
type: docs
description: >
  Setting the millimeters per pixel value in OpenPnP
---

This next step calibrates the relationship between pixels and millimeters to make our cameras more accurate. But first, we're going to add some nozzle tips to our nozzles.

## Mounting Nozzle Tips

1. Lubricate both of your brass nozzles using the included packet of SuperLube. We do this before shipping, but adding a bit extra ensures that mounting nozzle tips doesn't damage the rubber O-rings around the holder.
  ![Apply Lubricant to holder](images/apply-super-lube.jpg)

1. Identify your machine's nozzle tips. They're mounted in the rack on your staging plate.
   ![](../../../semi-assembly-3-1/mounting-staging-plates-3-1/images/nozzle-tip-location.JPG)

1. Remove the nozzle tips labeled `N045` and `N24` from the rack.

1. In OpenPnP, navigate to `Machine Setup > Heads > ReferenceHead H1 > Nozzles > ReferenceNozzle N1` and select the `Nozzle Tips` tab, and check the checkbox in the `Loaded?` column for the `N045` row.
  ![](images/n045-on-n1.png)

1. Your machine will jog the head to the front of the machine for easy tip loading. Slide the N045 nozzle tip (the one with the smaller opening) onto the **left** nozzle (using red tubing). Rotate the nozzle tip as you mount it to the brass holder to ensure the grease works its way into the tip and around the O-rings. It should slide on and off easily after working it in.
   ![left nozzle has red tubing getting n045 tip, right has no tip](images/mountingn1.jpg)

1. Now, navigate to the `ReferenceNozzle N2` and select the `Nozzle Tips` tab. This time, check the checkbox in the `Loaded?` column for the `N24` row.
   ![](images/n24-on-n2.png)

2. Slide the N24 nozzle tip (the one with the larger opening) onto the **right** nozzle (using blue tubing). Rotate the nozzle tip as you mount it to the brass holder to ensure the grease works its way into the tip and around the O-rings. It should slide on and off easily after working it in.
   ![blue tubing right nozzle getting n24 tip, left already has n045](images/mountingn2.jpg)

!!! Tip
    We mounted these two nozzle tips because these two sizes can pick the vast majority of parts without requiring a nozzle tip swap. Because of this, we highly recommend leaving these two tips mounted by default, and only swapping a tip if these two are unable to pick a part you need (typically very heavy parts).

## Top Camera Calibration

1. Navigate to `Machine Setup > Heads > ReferenceHead H1`.
  ![Reviewing the ReferenceHead options](images/Select-Reference-Head-H1.png)

1. Click on the "Position Camera over location" icon button show below. This will move the top camera to where your datum board is mounted.
  ![Position top camera over homing fiducial](images/Position-camera-over-homing-fiducial.png)

1. Click on `Heads > ReferenceHeadH1 > Cameras > OpenPnPCaptureCamera Top`.
  ![Select the top camera](images/select-top-camera.png)

1. Go to the `General Configuration` tab.
  ![Go to the general configuration tab](images/general-configuration-tab.png)

1. Scroll down to `Units Per Pixel`.
  ![The top camera's units per pixel section](images/units-per-pixel-section.png)

1. Set the X and Y Object Dimensions to `5`.
  ![Set the object dimensions for automatic calibration](images/set-object-dimensions.png)

1. Jog the machine so that one of the golden guideline squares on the datum board are visible in the top camera's view. The whole square must be visible. Zoom out of the camera feed with the scroll wheel if necessary.
  ![The square guideline on the datum board](images/units-per-pixel-square-on-datum.png)

1.  Then click the `Measure` button.
  ![Click the measure button](images/click-measure-button.png)

1.  Click and drag in the camera view to create a box. Drag the box so that it lines up with the lines on the datum board; they are exactly 5mm x 5mm. Make sure that you are aligning the bounding box with the **center** of the lines as shown in the image below.
  ![Drag the box to the center of the outline square on the datum board.](images/Screen Shot 2022-05-19 at 12.30.48 PM.png)

    !!! Note "Squareness"
        Don't worry if the square fo the box doesn't perfectly align with the camera image. Any slight skew will be adjusted for duing jobs with fiducial calibration.

1.  Once you have it perfectly outlined, click the `Measure` button again. The new calibration numbers will populate the Units per Pixel fields. They should be relatively close to the default values.
  ![Confirm the test](images/confirm-pixel-per-mm.png)

1.  Click `Apply` to save the changes.
  ![Apply the new settings](images/apply-pixel-per-mm-settings.png)

1.  To confirm, drag the reticle on the top camera view to move the machine. The camera center should move exactly where you tell it to. If it's inaccurate, try doing the calibration again or tweaking the values in the fields.

## Bottom Camera Calibration

1. Rehome your machine using the home button.

2. Navigate to `Machine Setup > Cameras > OpenPnPCaptureCamera Bottom`, then select the `Position` tab.
   ![Go to the Position tab](images/bottom-position-tab.png)

1. In the drop down under `Machine Controls` on the left, select `Nozzle: N2` so that for any nozzle commands we run, OpenPnP knows to make them based on N2 and not N1.
   ![selecting n2 for control](images/select-n2.png)

2. Click on the "Position Nozzle Over Location" button
   ![Position nozzle over camera](images/position-nozzle-over-camera.png)

3. Use the jog controls to move the nozzle directly over the center of the bottom camera. Do not adjust the Z-axis.
   ![Jog the nozzle over the camera](images/jog-controls-bottom.png)
   ![Jog the nozzle over the camera](images/jogging-finished.png)

    !!! Tip "Adjusting Focus"
        Focus is adjusted before shipping, but if you'd like to fune tune your adjustment, you can twist the lens of the bottom camera. You'll need to loosen the set screw on the side to allow it to turn.

        ![Jog the nozzle over the camera](images/in-focus-nozzle.png)

4.  Go to the `General Configuration` tab.
   ![Go to the general configuration tab](images/general-configuration-bottom-tab.png)

5.  Scroll down to `Units Per Pixel`.
   ![The bottom camera's units per pixel section](images/units-per-pixel-section-bottom.png)

6.  Set the X and Y Object Dimensions to `4`.
  ![Set the object dimensions for calibration](images/set-object-dimensions-bottom.png)

1.  Then click the `Measure` button.
  ![Click the measure button](images/click-measure-bottom.png)

1.  A box with drag handles will appear in the camera viewfinder. Drag the bounding box around the nozzle tip so that it's perfectly tangent to the edges; they are exactly 4mm x 4mm.
  ![Drag the box to the edges of the nozzle.](images/measure-nozzle-mm-per-px.png)

1.  Once you have it perfectly outlined, click `Measure` again. New numbers should populate the Units per Pixel fields. They should be relatively close to the default values.
  ![Confirm the test](images/confirm-pixel-per-mm-bottom.png)

1.  Then click `Apply` to save the changes.
  ![Apply the new settings](images/apply-pixel-per-mm-settings-bottom.png)

1.  To confirm, drag the reticle on the bottom camera view to move the machine. The **nozzle tip** should move exactly where you tell it to. If it's inaccurate, try doing the calibration again or tweaking the values in the fields.

## Next Steps

Next is [Nozzle Offset Calibration](../6-nozzle-offset/index.md).
