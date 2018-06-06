project('lua', 'c', 'cpp', version: '5.3.4', license: 'mit')

cc = meson.get_compiler('c')

# Resolve dependencies.
system_deps = [
	cc.find_library('dl', required: false),
	cc.find_library('m', required: false)
]

if host_machine.system() == 'windows'
	readline_dep = []
else
	readline_dep = cc.find_library('readline')
endif

# Make sure we have the right definition when compiling as a shared library on Windows.
if get_option('default_library') != 'static' and host_machine.system() == 'windows'
	add_project_arguments('-DLUA_BUILD_AS_DLL', language: 'c')
	compile_args = [ '-DLUA_BUILD_AS_DLL' ]
else
	compile_args = []
endif

# Set all C sources to compile as C++ (if requested).
link_args = []

if get_option('lua_cpp')
	if cc.get_id() == 'msvc'
		add_project_arguments('/TP', '/EHa', language: 'c')
		compile_args += [ '/EHa' ]
	elif cc.get_id() == 'gcc' or cc.get_id() == 'clang'
		# TODO: Verify that this works for clang
		add_project_arguments('-x',  'c++', language: 'c')
		link_args = [ '-lstdc++' ]
	else
		error('Unsupported platform')
	endif
endif

subdir('src')

# Dependency definition.
lua_dep = declare_dependency(
	include_directories: include_directories('src'),
	link_with: lua,
	compile_args: compile_args,
)
