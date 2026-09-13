add_library(kvdb STATIC)
# Third-party code: its NSKeyedArchiver calls are upstream's to change.
target_compile_options(kvdb PRIVATE -Wno-deprecated-declarations)

file(GLOB _src CONFIGURE_DEPENDS vendor/kvdb/*.m)
target_sources(kvdb PRIVATE ${_src})

# kvdb exports vendor/kvdb/kvdb.h — include parent so <kvdb/kvdb.h> works
target_include_directories(kvdb PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/vendor")

target_link_libraries(kvdb PRIVATE "-framework Cocoa" sqlite3)
