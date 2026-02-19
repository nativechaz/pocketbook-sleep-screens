#### Pocketboook e-Reader Sleep/Lock Screens

This is for sharing images I have created for use on a Pocketbook e-reader. To start, I have uploaded both the portrait and landscape versions of the images I created using “The Great Wave off Kanagawa” using a [tutorial](https://www.reddit.com/r/pocketbook/comments/1qkutiw/custom_sleep_screenlogo_on_any_pocketbook/) created by [u/Lefc1u](https://www.reddit.com/user/Lefc1u/) on Reddit.

These images are provided free for personal use. You are not allowed to sell these images individually or as part of a collection.

##### DISCLAIMER

This is just an overview of how I created images to use on my Pocketbook Verse Pro. I am very comfortable working in the command line of my Terminal, and know what I can or cannot (or should not) do. You may know more or you may know less, but know that I cannot guarantee that fiddling with this will ensure the safety of the internal workings of your device. Use at your own risk.

##### Brief summary of the tutorial steps:

1. Images must match the resolution of the device. For a Verse Pro, that is 1072x1448 pixels (portrait) or 1448x1072 (landscape)
2. Any part of the image meant to be transparent must use the color #808040 or rgb(128, 128, 64) as the devices treat *this* color transparent but don't actually support an PNG-esque alpha-channel transparency layer. (You can see this in my thumbnail images).
3. Images must be 24-bit BMP files.
4. Images must be named precisely: `taskmgr_lock_background.bmp` and `taskmgr_lock_background_landscape.bmp`
5. Images must be copied to the following folder on the device: `/system/resources/Line`

##### Notes about transparency when creating the image

For my *Great Wave* images, I used Affinity Designer 2 to create the initial PNG file that I later used ImageMagick to convert to a BMP. When erasing the background bits I didn't want in the image, I had to set the Hardness to 100% so that I wasn't inadvertently creating a soft or semi-transparent edge to the image. The image is hard pixels all the way around.

##### Notes about 24-bit BMP files

- If you ask ImageMagick to confirm the image details, it will report that the BMP is "8-bit", but it really means "8 bits per channel: R, G, and B". So it really is a 24-bit image. In Terminal on macOS `file taskmgr_lock_background.bmp` will report: `taskmgr_lock_background.bmp: PC bitmap, Windows 3.x format, 1072 x 1448 x 24, image size 4656768, resolution 2835 x 2835 px/m, cbSize 4656822, bits offset 54`
- Since the bitmap files are uncompressed, they will be larger than a JPEG. So my Verse Pro images are (1072 x 1448 x 3) + 54 bytes = 4,646,822 bytes.

##### Note about the destination folder

You want to be very careful about dealing with the `/system` folder. You don't want to accidentally overwrite the whole thing because you were trying to copy something **into** it and not **over** it. If you're not using the command line, and you're dragging folders here and there, you might see the `system` folder. But I was using the command line, and could use the following process:

```bash
# Change to the device's root directory
cd  /Volumes/PB634

# Create the `resources/Line` subdirectories with the root if they don't exist
mkdir -p /system/resources/Line

# Change to the destination directory
cd /system/resrouces/Line

# Copy my BMP images from the folder on my Desktop to the current directory
cp ~/Desktop/great-wave/*.bmp .
```

Note that `PB634` is just the default device designation when I plugged in the Verse Pro to my Mac. If you have a different device, you should see a different `PBxxx`.
