# RT-Thread building script for JerryScript

import os
from building import *
Import('Env')

# get current directory
cwd = GetCurrentDir()

jerry_core_dir = 'jerryscript/jerry-core'

jerry_core = Glob(jerry_core_dir + '/*.c')
jerry_core += Glob(jerry_core_dir + '/api/*.c')
jerry_core += Glob(jerry_core_dir + '/debugger/*.c')
jerry_core += Glob(jerry_core_dir + '/ecma/base/*.c')
jerry_core += Glob(jerry_core_dir + '/ecma/builtin-objects/*.c')
jerry_core += Glob(jerry_core_dir + '/ecma/builtin-objects/typedarray/*.c')
jerry_core += Glob(jerry_core_dir + '/ecma/operations/*.c')
jerry_core += Glob(jerry_core_dir + '/jcontext/*.c')
jerry_core += Glob(jerry_core_dir + '/jmem/*.c')
jerry_core += Glob(jerry_core_dir + '/jrt/*.c')
jerry_core += Glob(jerry_core_dir + '/lit/*.c')
jerry_core += Glob(jerry_core_dir + '/parser/js/*.c')
jerry_core += Glob(jerry_core_dir + '/parser/regexp/*.c')
jerry_core += Glob(jerry_core_dir + '/vm/*.c')

jerry_ext_dir = 'jerryscript/jerry-ext'

jerry_ext = Glob(jerry_ext_dir + '/arg/*.c')
jerry_ext += Glob(jerry_ext_dir + '/handler/*.c')
jerry_ext += Glob(jerry_ext_dir + '/include/*.c')
jerry_ext += Glob(jerry_ext_dir + '/module/*.c')

src = jerry_core + jerry_ext

CPPPATH = [cwd]

jerry_core_dir = cwd + '/jerryscript/jerry-core'

CPPPATH += [jerry_core_dir + '/api']
CPPPATH += [jerry_core_dir + '/debugger']
CPPPATH += [jerry_core_dir + '/ecma/base']
CPPPATH += [jerry_core_dir + '/ecma/builtin-objects']
CPPPATH += [jerry_core_dir + '/ecma/builtin-objects/typedarray']
CPPPATH += [jerry_core_dir + '/ecma/operations']
CPPPATH += [jerry_core_dir + '/include']
CPPPATH += [jerry_core_dir + '/jcontext']
CPPPATH += [jerry_core_dir + '/jmem']
CPPPATH += [jerry_core_dir + '/jrt']
CPPPATH += [jerry_core_dir + '/lit']
CPPPATH += [jerry_core_dir + '/parser/js']
CPPPATH += [jerry_core_dir + '/parser/regexp']
CPPPATH += [jerry_core_dir + '/vm']

jerry_ext_dir = cwd + '/jerryscript/jerry-ext'

CPPPATH += [jerry_ext_dir + '/arg']
CPPPATH += [jerry_ext_dir + '/handler']
CPPPATH += [jerry_ext_dir + '/include']
CPPPATH += [jerry_ext_dir + '/module']

LOCAL_CCFLAGS = ''
if Env['CC'] == 'keil':
    LOCAL_CCFLAGS += ' --gnu'
elif Env['CC'].find('gcc') != -1:
    LOCAL_CCFLAGS += ' -std=c11'

CPPDEFINES = ['JERRY_JS_PARSER', 'JERRY_ENABLE_EXTERNAL_CONTEXT']

if GetDepend('PKG_JERRY_ENABLE_ERROR_MESSAGES'):
    CPPDEFINES += ['JERRY_ENABLE_ERROR_MESSAGES']

if GetDepend('PKG_JERRY_ENABLE_LOGGING'):
    CPPDEFINES += ['JERRY_ENABLE_LOGGING']
    
if GetDepend('PKG_JMEM_STATS'):
    CPPDEFINES += ['JMEM_STATS']

if GetDepend('PKG_CONFIG_DISABLE_ES2015'):
    CPPDEFINES += ['CONFIG_DISABLE_ES2015']

group = DefineGroup('JerryScript', src, depend = ['PKG_USING_JERRYSCRIPT'], CPPPATH = CPPPATH, 
    CPPDEFINES = CPPDEFINES, LOCAL_CCFLAGS = LOCAL_CCFLAGS)

group = group + SConscript(os.path.join('rtthread-port', 'SConscript'))

Return('group')
