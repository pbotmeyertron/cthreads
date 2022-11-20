# cthreads
Single-header, C11 threads implementation.

This is a complete implementation of the cross-platform C11 threads library. It can be used in lieu of pthreads on Unix platforms, and Win32 threads on Windows. It has been thoroughly tested on x86 and ARM platforms. The API contains the following functions:
 - call_once() 
 - cnd_broadcast()	
 - cnd_destroy()	
 - cnd_init()	
 - cnd_signal()	
 - cnd_timedwait()	
 - cnd_wait()	
 - mtx_destroy()	
 - mtx_init()	
 - mtx_lock()
 - mtx_timedlock()	
 - mtx_trylock()	
 - mtx_unlock()	
 - thrd_create()	
 - thrd_current()	
 - thrd_detach()	
 - thrd_equal()	
 - thrd_exit()	
 - thrd_join()	
 - thrd_yield()	
 - tss_create()	
 - tss_delete()	
 - tss_get()	
 - tss_set()	

## Note:
This project is a fork of tinycthread: https://github.com/tinycthread/tinycthread
The main difference is that this is a single-header implementation of the library with some minor changes. The authors of that project have done the vast majority of the work here and deserve all of the credit. I just wanted a single-header, drop-in replacement for cross-platform development. If you are also tired of waiting for Microsoft to implement a C11-compliant compiler, then this is for you.

# List of changes:
 - Single header; drop-in replacement ready for C11 threads
 - In mtx_timedlock() the __restrict keyword was added to better match the C11 threads API.
 - In cnd_timedwait() the __restrict keyword was added to better match the C11 threads API.
 - Changed thread exit and error codes to enums to be in line with the C11 standard
 - Changed mutex codes from defines to enums to match the C11 standard
 - Added explicit support for Clang
 - Removed the emulation for timespec_get, as most platforms support this function now (time.h). 
 - Removed some of the #defines (NULL, TRUE, FALSE) in favor of stddef.h

## Minor Bug Fixes
 - Refactored mtx_trylock() int two functions: mtx_trylock() and mtx_trylock_acquire_win32(), because there was the possibility of
   a locking side-effect being introduced because mtx->mHandle.cs was not getting properly released.
