# How can I set an icon for my Android application?

![appicon](https://user-images.githubusercontent.com/51777024/86588600-a19caf80-bfa9-11ea-8ded-83cc017d955d.jpg)

# Step1:If you intend on your application being available on a large range of devices, you should place your application icon into the different res/drawable... folders provided. In each of these folders, you should include a 48dp sized icon:

* drawable-ldpi (120 dpi, Low density screen) - 36px x 36px
* drawable-mdpi (160 dpi, Medium density screen) - 48px x 48px
* drawable-hdpi (240 dpi, High density screen) - 72px x 72px
* drawable-xhdpi (320 dpi, Extra-high density screen) - 96px x 96px
* drawable-xxhdpi (480 dpi, Extra-extra-high density screen) - 144px x 144px
* drawable-xxxhdpi (640 dpi, Extra-extra-extra-high density screen) - 192px x 192px

# Step2:You may then define the icon in your AndroidManifest.xml file as such
