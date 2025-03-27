project(
    'FACE',
    'fortran',
    version: '1.3.3',
    default_options: [
        'fortran_std=f2008',
    ]
)

fc = meson.get_compiler('fortran')


ascii_code = '''
program ascii_support;
     integer, parameter :: ascii = selected_char_kind('ascii');
     if(ascii < 0) stop 1;
end program ascii_support
'''
ascii_supported = fc.run(ascii_code, name: 'ascii support')

if ascii_supported.returncode() == 0
    add_project_arguments('-DASCII_SUPPORTED', language : 'fortran')
endif

ascii_neq_code = '''
program ascii_neq_default;
     integer, parameter :: ascii = selected_char_kind('ascii');
     integer, parameter :: default = selected_char_kind('default');
     if(ascii == default) stop 1;
end program ascii_neq_default
'''
ascii_neq_default = fc.run(ascii_neq_code, name: 'ascii neq default')
if ascii_neq_default.returncode() == 0
    add_project_arguments('-DASCII_NEQ_DEFAULT', language : 'fortran')
endif

ucs4_code = '''
program ucs4_support;
     integer, parameter :: ucs4 = selected_char_kind('iso_10646');
     if(ucs4 < 0) stop 1;
end program ucs4_support
'''
ucs4_supported = fc.run(ucs4_code, name: 'ucs4 support')
if ucs4_supported.returncode() == 0
    add_project_arguments('-DUCS4_SUPPORTED', language : 'fortran')
endif

default_lib_type = get_option('default_library')
if default_lib_type != 'static'
    add_project_arguments('-fpic', language : 'fortran')
endif

fc_id = fc.get_id()

if 'intel' in fc_id
    add_project_arguments('-fpp', language: 'fortran')
    add_project_arguments('-assume realloc_lhs', language : 'fortran')
elif 'gcc' in fc_id
    add_project_arguments('-cpp', language: 'fortran')
    add_project_arguments('-frealloc-lhs', language : 'fortran')
endif

subdir('src/lib')