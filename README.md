# JUCE Template

Basic JUCE template project.

## License
GPL-3.0

# Things to update
## /cmake/cpm.cmake
Update: set(CPM_DOWNLOAD_VERSION 0.42.0) to latest CPM Version on GitHub

## plugin/CMakeLists.txt
Update YourPluginName in 2 places
Update juce_add_plugin with options required
May need to set source and include files for additional files
Configure target_link_libraries_system 
Get AI to generate unique PLUGIN_CODE - check against plugin_codes_used.txt
Update plugin_codes_used.txt in JUCE_Template and push to Github

## CMakeLists.txt
Update project(SBSAudioPluginTemplate)
Update cpmaddpackage with latest JUCE Version and GoogleTest version 

## plugin/include/YourPluginName
rename with plugin name

## Best to create and push repository yourself

## Create and build terminal commands
cmake -S . -B build
cmake --build build