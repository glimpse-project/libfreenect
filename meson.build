project('libfreenect', 'c', license: [ 'Apache 2.0', 'GPL 2.0'])

version='0.6.0'

compiler = meson.get_compiler('c')

m_dep = compiler.find_library('m', required : false)
libusb = dependency('libusb-1.0', required: false)


if libusb.found()

libfreenect_src = [
    'src/audio.c',
    'src/cameras.c',
    'src/core.c',
    'src/flags.c',
    'src/loader.c',
    'src/registration.c',
    'src/tilt.c',
    'src/usb_libusb10.c',
]

freenect_lib = library('freenect', libfreenect_src,
        version: version,
        include_directories: include_directories('include'),
        dependencies: [ libusb ]
)
freenect_dep = declare_dependency(link_with: freenect_lib,
                                  include_directories: include_directories('include'))

fakenect_record_src = [
    'fakenect/parson.c',
    'fakenect/record.c',
]

executable('fakenect-record', fakenect_record_src,
           include_directories: include_directories('include', 'src', 'fakenect/fake-libusb'),
           dependencies: [ freenect_dep, m_dep ])

endif # found libusb

libfakenect_src = [
    'fakenect/fakenect.c',
    'fakenect/parson.c',
    'src/registration.c',
]

fakenect_lib = library('fakenect', libfakenect_src,
                       version: version,
                       include_directories: include_directories('include', 'src', 'fakenect/fake-libusb'),
                       dependencies: [ m_dep ]
)
fakenect_dep = declare_dependency(link_with: fakenect_lib,
                                  include_directories: include_directories('include'))


