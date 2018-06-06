lua_src = [
	'lapi.c',
	'lauxlib.c',
	'lbaselib.c',
	'lbitlib.c',
	'lcode.c',
	'lcorolib.c',
	'lctype.c',
	'ldblib.c',
	'ldebug.c',
	'ldo.c',
	'ldump.c',
	'lfunc.c',
	'lgc.c',
	'linit.c',
	'liolib.c',
	'llex.c',
	'lmathlib.c',
	'lmem.c',
	'loadlib.c',
	'lobject.c',
	'lopcodes.c',
	'loslib.c',
	'lparser.c',
	'lstate.c',
	'lstring.c',
	'lstrlib.c',
	'ltable.c',
	'ltablib.c',
	'ltm.c',
	'lundump.c',
	'lutf8lib.c',
	'lvm.c',
	'lzio.c',
]

# Expose library target.
lua = library('lua',
	lua_src,
	include_directories: include_directories('.'),
	dependencies: system_deps,
	link_args: link_args
)

# Define targets for the interpreter and compiler.
executable('luai', 'lua.c',
	link_with: lua,
	dependencies: readline_dep
)

# The compiler requires lua to be built as a static lib.
if get_option('default_library') == 'static'
	executable('luac', 'luac.c', 
		link_with: lua
	)
endif
