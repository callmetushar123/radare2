subdir('d')

r_asm_sources = [
  'asm.c',
  'aop.c',
  'acode.c',
  'aplugs.c',
  'binutils_as.c',
  join_paths('p','asm_null.c'),
  join_paths('p','asm_arm_as.c'),
  join_paths('p','asm_arm.c'),
  #join_paths('p','asm_arm_winedbg.c'),
  #join_paths('p','asm_gas.c'),
  'arch/arm/gnu/floatformat.c',
  join_paths('p','asm_ppc_as.c'),
  join_paths('p','asm_x86_as.c'),
  join_paths('p','asm_x86_nasm.c'),
  join_paths('p','asm_x86_nz.c'),
  # join_paths('p','asm_z80.c'),
  join_paths('arch','arm','armass.c'),
  join_paths('arch','arm','armass64.c'),
#join_paths('arch','arm','winedbg','be_arm.c'),
  join_paths('arch','avr','avr_disasm.c'),
  join_paths('arch','avr','format.c'),
  join_paths('arch','avr','disasm.c'),
  join_paths('arch','avr','assemble.c'),
  #join_paths('arch','hexagon','gnu','hexagon-dis.c'),
  #join_paths('arch','hexagon','gnu','hexagon-opc.c'),
  #join_paths('arch','hexagon','gnu','safe-ctype.c'),
  #join_paths('arch','i8080','i8080dis.c'),
#join_paths('arch','lanai','gnu','lanai-dis.c'),
#  join_paths('arch','lanai','gnu','lanai-opc.c'),
  join_paths('arch','v810','v810_disas.c'),
  # join_paths('arch','whitespace','wsdis.c'),
  #join_paths('arch','z80','expressions.c'),
  # join_paths('arch','z80','z80.c'),
  #join_paths('arch','z80','z80asm.c'),
  #join_paths('arch','jdh8','jdh8dis.c'),
]

r_asm_inc = [
  platform_inc,
  include_directories(
    join_paths('..','..','shlr'),
    join_paths('arch','include'),
    join_paths('arch'),
    join_paths('arch','h8300'),
    join_paths('arch','v810'),
  )
]

if get_option('sdb_cgen')
  r_asm_sources += r_asm_d_sources
endif

r_asm = library('r_asm', r_asm_sources,
  include_directories: r_asm_inc,
  c_args: library_cflags,
  dependencies: [
    r_util_dep,
    r_syscall_dep,
    r_parse_dep,
    r_lang_dep,
    r_arch_dep,
    r_flag_dep,
    r_socket_dep,
    capstone_dep,
    java_dep
  ],
  install: true,
  implicit_include_directories: false,
  install_rpath: rpath_lib,
  soversion: r2_libversion
)

r_asm_dep = declare_dependency(link_with: r_asm,
                               include_directories: r_asm_inc)

if get_option('blob')
r_asm_static = static_library('r_asm_static', r_asm_sources,
  include_directories: r_asm_inc,
  c_args: library_cflags,
  dependencies: [
    r_util_static_dep,
    r_arch_static_dep,
    r_syscall_static_dep,
    r_parse_static_dep,
    r_lang_static_dep,
    r_flag_static_dep,
    r_socket_static_dep,
    capstone_dep,
    java_static_dep
  ],
  install: true,
  implicit_include_directories: false,
  install_rpath: rpath_lib,
)

r_asm_static_dep = declare_dependency(link_with: r_asm_static,
                               include_directories: r_asm_inc)
endif

pkgconfig_mod.generate(r_asm,
  subdirs: 'libr',
  version: r2_version,
  name: 'r_asm',
  filebase: 'r_asm',
  libraries: pkgcfg_sanitize_libs,
  requires: [
    'r_util',
    'r_syscall',
    'r_parse',
    'r_lang',
    'r_flag',
    'r_arch',
    'r_socket'
  ],
  description: 'radare foundation libraries'
)
