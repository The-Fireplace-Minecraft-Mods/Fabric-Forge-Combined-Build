### About
This is a generic workspace for developing a Minecraft mod for [Forge](https://www.minecraftforge.net/) and [Fabric](https://fabricmc.net/), as well as tools for packaging the release as one jar and publishing it. Note that this is *not* a way to avoid coding your mod twice, it must still be coded for each modloader.

### Advantages
- Users will not have to go reading through filenames to find which file is for which loader.
- You can view both versions of the mod within one workspace.
- Common, loader-independent files can be developed and used with both versions of the mod.
- Common files don't have to be kept synced between two folders.

### Known caveats
- Currently no task to automatically generate IDEA workspace
- Designed around a specific file naming scheme for the output jars, this can be changed at some point in the future but priority was given to getting this working first.
- Currently no tasks to sign the jar or publish to maven.
- Files for Fabric and Forge must not have the same filename and package. To avoid this problem, I recommend having all your Fabric code in a fabric package and Forge code in a forge package.
- IDEA considers the common folder to belong to one of the two other modules, meaning it allows you to interact with files from one loader or the other when editing in the common folder. Be careful not to do this because **both** modules compile the common sources.

### Setup (Instructions written with IntelliJ Idea in mind - Eclipse or other IDE users may have to do steps 2 & 5 differently):
1. Import the root build.gradle into your IDE as a gradle project.
2. In IDEA, go to File>New>Module from Existing Sources… and choose `fabric/build.gradle` Repeat this step for `forge/build.gradle`.
3. To set up your publishing, you will want to find or create your `gradle.properties` in `GRADLE_USER_HOME` and add `curseForgeApiKey=YOUR_API_KEY_HERE`. If you're like me and have 
an account on mods.io and hope they will update it to support 1.13+, you can also add that API key with `modsioApiKey=YOUR_API_KEY_HERE`
4. ~~If you wish to sign your jar~~ TODO

Run configurations are included when using IDEA, they are Forge Client, Forge Server, Fabric Client, and Fabric Server.

### Build:

Run [gradle] in the repository root: `./gradlew[.bat] build`

### Build & Publish:
**important**: Do not run the `curseforge` task directly or an empty jar will be published. Use `cfpublish` instead.

Run [gradle] in the repository root: `./gradlew[.bat] cfpublish [uploadToModsio]`

### Common Problems and Solutions:
- Problem: IDEA shows an error at `FileTree` in the main build.gradle. Solution: Open the `Gradle` tab and press the button for `Reimport all gradle projects` ![Reimport icon](https://i.imgur.com/UneSl68.png)
- Problem: CurseForge doesn't allow tagging files as Fabric and Forge from the web interface. Solution: Upload the files using the `cfpublish` task.
- Problem: fabric runClient crashes with `java.lang.ExceptionInInitializerError ... Caused by: java.lang.RuntimeException: java.lang.UnsatisfiedLinkError: Failed to locate library: liblwjgl.so`. Solution: Open a terminal in the fabric directory and run `./gradlew idea`. I recommend deleting the three files it generates in that folder.
