face_srcs = [
    'face.f90',
]

face_include_dir = include_directories('.')


libface = library(
    'libface',
    face_srcs,
)

libface_dep = declare_dependency(
        include_directories: face_include_dir,
        link_with: libface,
)