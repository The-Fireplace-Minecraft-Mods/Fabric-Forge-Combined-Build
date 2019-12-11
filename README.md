### About
This is a generic workspace for developing a Minecraft mod for [Forge](https://www.minecraftforge.net/) and [Fabric](https://fabricmc.net/), as well as tools for packaging the release as one jar and publishing it.

There are several advantages to making your release this way: Users will not have to go reading through filenames to find which file is for which loader, and you can view both versions of the mod within one workspace. Note that this is *not* a way to avoid coding your mod twice, it must still be coded for each modloader.

### Known caveats
- Currently no task to automatically generate IDEA workspace and run configurations
- Designed around a specific file naming scheme for the output jars, this can be changed at some point in the future but priority was given to getting this working first.
- Currently no tasks to sign the jar or publish to maven.
- Files for Fabric and Forge must not have the same filename and package. To avoid this problem, I recommend having all your Fabric code in a fabric package and Forge code in a forge package.
### Setup (Instructions written with IntelliJ Idea in mind - Eclipse or other IDE users may have to do step 2 differently):
1. Import the root build.gradle into your IDE as a gradle project.
2. In IDEA, go to File>New>Module from Existing Sources… and choose `fabric/build.gradle` Repeat this step for `forge/build.gradle`.
3. To set up your publishing, you will want to find or create your `gradle.properties` in `GRADLE_USER_HOME` and add `curseForgeApiKey=YOUR_API_KEY_HERE`. If you're like me and have 
an account on mods.io and hope they will update it to support 1.13+, you can also add that API key with `modsioApiKey=YOUR_API_KEY_HERE`
4. ~~If you wish to sign your jar~~ TODO
5. ~~Run configurations~~ TODO

### Build:

Run [gradle] in the repository root: `./gradlew[.bat] build`

### Build & Publish:
Run [gradle] in the repository root: `./gradlew[.bat] build curseforge [uploadToModsio]`
