def merge_dicts(x, y):
  z = x.copy()
  z.update(y)
  return z

jansson_config_macos = '''
#ifndef JANSSON_CONFIG_H
#define JANSSON_CONFIG_H

#ifdef __cplusplus
#define JSON_INLINE inline
#else
#define JSON_INLINE inline
#endif

#define JSON_INTEGER_IS_LONG_LONG 1

#define JSON_HAVE_LOCALECONV 1
#define JSON_PARSER_MAX_DEPTH 2048

#endif
'''

jansson_private_config_macos = '''
#ifndef JANSSON_PRIVATE_CONFIG_H
#define JANSSON_PRIVATE_CONFIG_H

#define HAVE_ATOMIC_BUILTINS 1
#define HAVE_CLOSE 1
#define HAVE_DLFCN_H 1
#define HAVE_FCNTL_H 1
#define HAVE_GETPID 1
#define HAVE_GETTIMEOFDAY 1
#define HAVE_INTTYPES_H 1
#define HAVE_LOCALECONV 1
#define HAVE_LOCALE_H 1
#define HAVE_LONG_LONG_INT 1
#define HAVE_MEMORY_H 1
#define HAVE_OPEN 1
#define HAVE_READ 1
#define HAVE_SCHED_H 1
#define HAVE_SCHED_YIELD 1
#define HAVE_STDINT_H 1
#define HAVE_STDLIB_H 1
#define HAVE_STRINGS_H 1
#define HAVE_STRING_H 1
#define HAVE_STRTOLL 1
#define HAVE_SYNC_BUILTINS 1
#define HAVE_SYS_PARAM_H 1
#define HAVE_SYS_STAT_H 1
#define HAVE_SYS_TIME_H 1
#define HAVE_SYS_TYPES_H 1
#define HAVE_UNISTD_H 1
#define HAVE_UNSIGNED_LONG_LONG_INT 1
#define INITIAL_HASHTABLE_ORDER 3
#define LT_OBJDIR \\\".libs/\\\"
#define PACKAGE \\\"jansson\\\"
#define PACKAGE_BUGREPORT \\\"petri@digip.org\\\"
#define PACKAGE_NAME \\\"jansson\\\"
#define PACKAGE_STRING \\\"jansson 2.10\\\"
#define PACKAGE_TARNAME "jansson"
#define PACKAGE_URL \\\"\\\"
#define PACKAGE_VERSION \\\"2.10\\\"
#define STDC_HEADERS 1
#define USE_URANDOM 1
#define USE_WINDOWS_CRYPTOAPI 1
#define VERSION \\\"2.10\\\"

#endif
'''

genrule(
  name = 'jansson-config',
  out = 'jansson_config.h',
  cmd = 'echo "' + jansson_config_macos + '" > $OUT',
)

genrule(
  name = 'jansson-private-config',
  out = 'jansson_private_config.h',
  cmd = 'echo "' + jansson_private_config_macos + '" > $OUT',
)

cxx_library(
  name = 'jansson',
  header_namespace = '',
  exported_headers = merge_dicts(subdir_glob([
    ('src', 'jansson.h'),
  ]), {
    'jansson_config.h': ':jansson-config',
  }),
  headers = merge_dicts(subdir_glob([
    ('src', '**/*.h'),
  ]), {
    'jansson_private_config.h': ':jansson-private-config',
  }),
  srcs = glob([
    'src/**/*.c',
  ]),
  compiler_flags = [
    '-DHAVE_CONFIG_H',
  ],
  visibility = [
    'PUBLIC',
  ],
)
