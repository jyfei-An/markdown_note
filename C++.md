#  判断文件夹是否存在并创建文件夹

```C++
fs::path log_dir(fs::current_path().generic_string() +u8"\\Logs");
if (!fs::exists(log_dir) || !fs::is_directory(log_dir))
{
    fs::create_directory(log_dir);
}
```

# 加载动态库

## linux加载动态库

```
http://manpages.courier-mta.org/htmlman3/dlopen.3.html
```

```C++
#include <stdio.h>
#include <stdlib.h>
#include <dlfcn.h>
#include <gnu/lib-names.h>  /* Defines LIBM_SO (which will be a
                               string such as "libm.so.6") */
int
main(void)
{
    void *handle;
    double (*cosine)(double);
    char *error;

    handle = dlopen(LIBM_SO, RTLD_LAZY);
    if (!handle) {
        fprintf(stderr, "%s\n", dlerror());
        exit(EXIT_FAILURE);
    }

    dlerror();    /* Clear any existing error */

    cosine = (double (*)(double)) dlsym(handle, "cos");

    /* According to the ISO C standard, casting between function
       pointers and 'void *', as done above, produces undefined results.
       POSIX.1-2003 and POSIX.1-2008 accepted this state of affairs and
       proposed the following workaround:

           *(void **) (&cosine) = dlsym(handle, "cos");

       This (clumsy) cast conforms with the ISO C standard and will
       avoid any compiler warnings.

       The 2013 Technical Corrigendum to POSIX.1-2008 (a.k.a.
       POSIX.1-2013) improved matters by requiring that conforming
       implementations support casting 'void *' to a function pointer.
       Nevertheless, some compilers (e.g., gcc with the '-pedantic'
       option) may complain about the cast used in this program. */

    error = dlerror();
    if (error != NULL) {
        fprintf(stderr, "%s\n", error);
        exit(EXIT_FAILURE);
    }

    printf("%f\n", (*cosine)(2.0));
    dlclose(handle);
    exit(EXIT_SUCCESS);
}
```

## windows加载动态库

动态库静态库使用方法详解

```
https://www.cnblogs.com/LuckCoder/p/11208158.html
```

```
#include "stdafx.h"
#include <windows.h>

int main()
{
    HMODULE hmodule  = LoadLibrary("deftest.dll");
    if (hmodule)
    {
        typedef void(*LoadProc)();
        LoadProc loadproc = (LoadProc)GetProcAddress(hmodule, "MyPrint");
        if (loadproc)
        {
            loadproc();
            FreeLibrary(hmodule);
        }
        else
        {
            FreeLibrary(hmodule);
        }
    }
    return 0;
}
```