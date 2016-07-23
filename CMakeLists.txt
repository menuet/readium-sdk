###################
# project settings

project(readium-sdk CXX)
cmake_minimum_required(VERSION 2.8.11)


###################
# options

set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_CONFIGURATION_TYPES Debug Release)
set(READIUM_PLATFORM "Windows")


###################
# computed settings

if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang" OR
    "${CMAKE_CXX_COMPILER_ID}" STREQUAL "AppleClang" OR
    "${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU" OR
    "${CMAKE_CXX_COMPILER_ID}" STREQUAL "Intel")
#    add_definitions(-std=c++11 -fPIC -fvisibility=hidden -fvisibility-inlines-hidden)
    set(READIUM_LIBRARY_TYPE STATIC)
elseif("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
    set(READIUM_LIBRARY_TYPE SHARED)
endif()

set(READIUM_ROOT_DIR "${PROJECT_SOURCE_DIR}")
set(READIUM_COMMON_SOURCE_DIR "${READIUM_ROOT_DIR}/ePub3")
set(READIUM_PLATFORM_SOURCE_DIR "${READIUM_ROOT_DIR}/Platform/${READIUM_PLATFORM}")


###################
# sources

set(
    READIUM_EPUB_SOURCE_FILES
    ${READIUM_COMMON_SOURCE_DIR}/_compiler.h
    ${READIUM_COMMON_SOURCE_DIR}/_config.h
    ${READIUM_COMMON_SOURCE_DIR}/_platform.h
    ${READIUM_COMMON_SOURCE_DIR}/base.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/archive.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/archive.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/archive_xml.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/archive_xml.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/cfi.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/cfi.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/container.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/container.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/content_handler.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/content_handler.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/content_module.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/content_module_manager.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/content_module_manager.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/credential_request.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/credential_request.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/encryption.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/encryption.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/epub_collection.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/epub_collection.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/epub3.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/filter.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/filter_chain.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/filter_chain.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/filter_chain_byte_stream.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/filter_chain_byte_stream.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/filter_chain_byte_stream_range.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/filter_chain_byte_stream_range.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/filter_manager.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/filter_manager.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/filter_manager_impl.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/filter_manager_impl.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/font_obfuscation.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/font_obfuscation.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/glossary.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/glossary.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/initialization.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/initialization.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/library.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/library.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/link.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/link.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/manifest.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/manifest.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/media_support_info.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/media_support_info.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/media-overlays_smil_data.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/media-overlays_smil_data.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/media-overlays_smil_model.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/media-overlays_smil_model.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/media-overlays_smil_utils.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/nav_element.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/nav_point.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/nav_point.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/nav_table.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/nav_table.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/object_preprocessor.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/object_preprocessor.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/package.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/package.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/PassThroughFilter.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/PassThroughFilter.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/property.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/property.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/property_extension.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/property_extension.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/property_holder.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/property_holder.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/signatures.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/signatures.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/spine.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/spine.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/switch_preprocessor.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/switch_preprocessor.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/user_action.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/xpath_wrangler.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/xpath_wrangler.h
    ${READIUM_COMMON_SOURCE_DIR}/ePub/zip_archive.cpp
    ${READIUM_COMMON_SOURCE_DIR}/ePub/zip_archive.h
    )

set(
    READIUM_GOOGLEURL_SOURCE_FILES
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/base/basictypes.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/base/logging.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/base/string16.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/base/string16.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/gurl.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/gurl.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_cpp11.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_etc.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_filesystemurl.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_fileurl.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_host.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_internal.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_internal.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_internal_file.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_ip.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_ip.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_mailtourl.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_path.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_pathurl.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_query.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_relative.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_stdstring.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_canon_stdurl.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_common.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_file.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_parse.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_parse.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_parse_file.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_parse_internal.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_test_utils.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_util.cc
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_util.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src/url_util_internal.h
    )

set(
    READIUM_UTILITIES_SOURCE_FILES
    ${READIUM_COMMON_SOURCE_DIR}/utilities/alphanum.hpp
    ${READIUM_COMMON_SOURCE_DIR}/utilities/basic.h
    ${READIUM_COMMON_SOURCE_DIR}/utilities/byte_buffer.cpp
    ${READIUM_COMMON_SOURCE_DIR}/utilities/byte_buffer.h
    ${READIUM_COMMON_SOURCE_DIR}/utilities/byte_stream.cpp
    ${READIUM_COMMON_SOURCE_DIR}/utilities/byte_stream.h
    ${READIUM_COMMON_SOURCE_DIR}/utilities/CPUCacheUtils_win.cpp
    ${READIUM_COMMON_SOURCE_DIR}/utilities/epub_locale.cpp
    ${READIUM_COMMON_SOURCE_DIR}/utilities/epub_locale.h
    ${READIUM_COMMON_SOURCE_DIR}/utilities/error_handler.cpp
    ${READIUM_COMMON_SOURCE_DIR}/utilities/error_handler.h
    ${READIUM_COMMON_SOURCE_DIR}/utilities/future.cpp
    ${READIUM_COMMON_SOURCE_DIR}/utilities/future.h
    ${READIUM_COMMON_SOURCE_DIR}/utilities/iri.cpp
    ${READIUM_COMMON_SOURCE_DIR}/utilities/iri.h
    ${READIUM_COMMON_SOURCE_DIR}/utilities/path_help.cpp
    ${READIUM_COMMON_SOURCE_DIR}/utilities/path_help.h
    ${READIUM_COMMON_SOURCE_DIR}/utilities/ring_buffer.cpp
    ${READIUM_COMMON_SOURCE_DIR}/utilities/ring_buffer.h
    ${READIUM_COMMON_SOURCE_DIR}/utilities/run_loop.h
    ${READIUM_COMMON_SOURCE_DIR}/utilities/run_loop_windows.cpp
    ${READIUM_COMMON_SOURCE_DIR}/utilities/utfstring.cpp
    ${READIUM_COMMON_SOURCE_DIR}/utilities/utfstring.h
    )

set(
    READIUM_XML_SOURCE_FILES
    ${READIUM_COMMON_SOURCE_DIR}/xml/tree/document.cpp
    ${READIUM_COMMON_SOURCE_DIR}/xml/tree/document.h
    ${READIUM_COMMON_SOURCE_DIR}/xml/tree/element.cpp
    ${READIUM_COMMON_SOURCE_DIR}/xml/tree/element.h
    ${READIUM_COMMON_SOURCE_DIR}/xml/tree/node.cpp
    ${READIUM_COMMON_SOURCE_DIR}/xml/tree/node.h
    ${READIUM_COMMON_SOURCE_DIR}/xml/tree/xpath.cpp
    ${READIUM_COMMON_SOURCE_DIR}/xml/tree/xpath.h
    ${READIUM_COMMON_SOURCE_DIR}/xml/utilities/base.cpp
    ${READIUM_COMMON_SOURCE_DIR}/xml/utilities/base.h
    ${READIUM_COMMON_SOURCE_DIR}/xml/utilities/io.cpp
    ${READIUM_COMMON_SOURCE_DIR}/xml/utilities/io.h
    ${READIUM_COMMON_SOURCE_DIR}/xml/validation/c14n.cpp
    ${READIUM_COMMON_SOURCE_DIR}/xml/validation/c14n.h
    ${READIUM_COMMON_SOURCE_DIR}/xml/validation/dtd.h
    ${READIUM_COMMON_SOURCE_DIR}/xml/validation/ns.cpp
    ${READIUM_COMMON_SOURCE_DIR}/xml/validation/ns.h
    ${READIUM_COMMON_SOURCE_DIR}/xml/validation/schema.cpp
    ${READIUM_COMMON_SOURCE_DIR}/xml/validation/schema.h
    )

set(
    READIUM_LIBZIP_SOURCE_FILES
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/mkstemp.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_add.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_add_dir.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_add_entry.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_buffer.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_close.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_delete.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_dir_add.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_dirent.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_discard.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_entry.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_err_str.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_error.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_error_clear.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_error_get.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_error_get_sys_type.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_error_strerror.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_error_to_str.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_extra_field.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_extra_field_api.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_fclose.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_fdopen.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_file_add.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_file_error_clear.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_file_error_get.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_file_get_comment.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_file_get_external_attributes.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_file_get_offset.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_file_rename.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_file_replace.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_file_set_comment.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_file_set_external_attributes.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_file_set_mtime.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_file_strerror.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_filerange_crc.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_fopen.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_fopen_encrypted.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_fopen_index.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_fopen_index_encrypted.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_fread.c
    #${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_fseek.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_get_archive_comment.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_get_archive_flag.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_get_compression_implementation.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_get_encryption_implementation.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_get_file_comment.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_get_name.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_get_num_entries.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_get_num_files.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_io_util.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_memdup.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_name_locate.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_new.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_open.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_rename.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_replace.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_set_archive_comment.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_set_archive_flag.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_set_default_password.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_set_file_comment.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_set_file_compression.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_set_name.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_begin_write.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_buffer.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_call.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_close.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_commit_write.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_crc.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_deflate.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_error.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_file.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_filep.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_free.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_function.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_is_deleted.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_layered.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_open.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_pkware.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_read.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_remove.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_rollback_write.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_seek.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_seek_write.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_stat.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_supports.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_tell.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_tell_write.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_window.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_write.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_zip.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_source_zip_new.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_stat.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_stat_index.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_stat_init.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_strerror.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_string.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_unchange.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_unchange_all.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_unchange_archive.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_unchange_data.c
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip_utf-8.c
    )

set_source_files_properties(${READIUM_LIBZIP_SOURCE_FILES} PROPERTIES LANGUAGE CXX)

set(
    READIUM_LIBZIP_SOURCE_FILES
    ${READIUM_LIBZIP_SOURCE_FILES}
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/Config.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zip.h
    ${READIUM_COMMON_SOURCE_DIR}/ThirdParty/libzip/zipint.h
    )

source_group(epub FILES ${READIUM_EPUB_SOURCE_FILES})
source_group(googleurl FILES ${READIUM_GOOGLEURL_SOURCE_FILES})
source_group(utilities FILES ${READIUM_UTILITIES_SOURCE_FILES})
source_group(xml FILES ${READIUM_XML_SOURCE_FILES})
source_group(libzip FILES ${READIUM_LIBZIP_SOURCE_FILES})

###################
# library

add_library(
    epub3new
    "${READIUM_LIBRARY_TYPE}"
    ${READIUM_EPUB_SOURCE_FILES}
    ${READIUM_GOOGLEURL_SOURCE_FILES}
    ${READIUM_UTILITIES_SOURCE_FILES}
    ${READIUM_XML_SOURCE_FILES}
    ${READIUM_LIBZIP_SOURCE_FILES}
    )

set_target_properties(epub3new PROPERTIES POSITION_INDEPENDENT_CODE TRUE)
set_target_properties(epub3new PROPERTIES VISIBILITY_INLINES_HIDDEN TRUE)

target_include_directories(
    epub3new
    PRIVATE
    "${READIUM_PLATFORM_SOURCE_DIR}/include"
    "${READIUM_PLATFORM_SOURCE_DIR}/ReadiumSDK/include"
    "${READIUM_COMMON_SOURCE_DIR}"
    "${READIUM_COMMON_SOURCE_DIR}/utilities"
    "${READIUM_COMMON_SOURCE_DIR}/ePub"
    "${READIUM_PLATFORM_SOURCE_DIR}/ReadiumSDK/Prebuilt/Include"
    "${READIUM_COMMON_SOURCE_DIR}/ThirdParty"
    "${READIUM_COMMON_SOURCE_DIR}/ThirdParty/google-url/src"
    "${READIUM_COMMON_SOURCE_DIR}/ThirdParty/utf8-cpp/include"
    "${READIUM_COMMON_SOURCE_DIR}/ThirdParty/icu4c/include"
    "${READIUM_PLATFORM_SOURCE_DIR}/include/libzip"
    )

target_compile_definitions(
    epub3new
    PRIVATE
    BUILDING_EPUB3
    HAVE_CONFIG_H
    _CRT_SECURE_NO_WARNINGS
    _CRT_NONSTDC_NO_DEPRECATE
    _SCL_SECURE_NO_WARNINGS
    _LIB
    _UNICODE
    )

target_link_libraries(
    epub3new
    PRIVATE
    "${READIUM_PLATFORM_SOURCE_DIR}/ReadiumSDK/Prebuilt/Lib/x86/libxml2_a.lib"
    "${READIUM_PLATFORM_SOURCE_DIR}/ReadiumSDK/Prebuilt/Lib/x86/zlib.lib"
    advapi32.lib
    ws2_32.lib
    user32.lib
    )

add_custom_command(
    TARGET epub3new
    PRE_BUILD
    COMMAND cscript MakeHeaders.js
    WORKING_DIRECTORY "${READIUM_PLATFORM_SOURCE_DIR}"
    COMMENT Copying header files to platform directory
    )

