find_package(Eigen3 REQUIRED)
if(Eigen3_FOUND)
	include_directories(${EIGEN3_INCLUDE_DIRS}) 
endif(Eigen3_FOUND)

# Crée des variables avec les fichiers à compiler
file(GLOB Source_Files *.cpp)
source_group("Source Files" FILES ${Source_Files})

file(GLOB Header_Files *.hpp)
source_group("Header Files" FILES ${Header_Files})

# On indique que l'on veut un exécutable "socp" compilé à partir des fichiers décrits par les variables SRCS et HEADERS
add_library(opinion_with_interactions ${Source_Files} ${Header_Files})
target_link_libraries(opinion_with_interactions socp)

set_target_properties(opinion_with_interactions PROPERTIES DEBUG_OUTPUT_NAME opinion_with_interactions_d)
set_target_properties(opinion_with_interactions PROPERTIES RELEASE_OUTPUT_NAME opinion_with_interactions)

install (TARGETS opinion_with_interactions
   		LIBRARY DESTINATION lib COMPONENT library
   		ARCHIVE DESTINATION lib COMPONENT library
   		RUNTIME DESTINATION bin COMPONENT library)
install(DIRECTORY ${CMAKE_SOURCE_DIR}/src/models/opinion_with_interactions
				DESTINATION "include/models" 
				FILES_MATCHING
				PATTERN "*.hpp"
				PATTERN "*.pdf"
				PATTERN "*.bib"
				)
