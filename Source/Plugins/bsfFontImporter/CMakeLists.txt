# Source files and their filters
include(CMakeSources.cmake)

# Packages
find_package(freetype REQUIRED)
	
# Target
add_library(bsfFontImporter SHARED ${BS_FONTIMPORTER_SRC})

# Common flags
add_common_flags(bsfFontImporter)

# Includes
target_include_directories(bsfFontImporter PRIVATE "./")

# Defines
target_compile_definitions(bsfFontImporter PRIVATE -DBS_FONT_EXPORTS -DUSE_FREETYPE2_STATIC)

# Libraries
## External lib: FreeType
target_link_libraries(bsfFontImporter ${freetype_LIBRARIES})

## Local libs
target_link_libraries(bsfFontImporter bsf)

# IDE specific
set_property(TARGET bsfFontImporter PROPERTY FOLDER Plugins)

# Install
install_bsf_target(bsfFontImporter)

conditional_cotire(bsfFontImporter)
