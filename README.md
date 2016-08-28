# wine-patches
Various wine patches mostly aimed at improving performance that aren't in wine or wine-staging (yet?).
May require CSMT patches (wine-staging).

### 0000-undo-ntdll-Heap-FreeLists.patch

Undoes the wine-staging "ntdll-Heap-Freelists" patch to allow patches 1, 3, and 5 to apply
cleanly to a pre-patched wine-staging tarball. Not needed on a clean tree or one that you
have patched yourself to exclude the aforementioned patch.

### 0001-ntdll-improve-heap-allocation-performance.patch

Improves heap allocation performance by balancing free lists and improving common bottlenecks.
Fixes Guild Wars 2 FPS decrease when it is running for a longer period of time and can almost
double the FPS in big fights (World Bosses, WvW, etc...) by reducing the overhead of the memory
allocator from ~30% CPU time to ~2%.

Don't use the "ntdll-Heap_FreeLists" patch from wine-staging when using this one (they have conflicting changes).

### 0003-ntdll-heap.c-align-everything-to-64-byte-to-reduce-f.patch

Align allocated memory to 64 byte boundaries to lessen false-sharing issues. May increase RAM usage.

### 0002-wined3d-use-SwitchToThread-and-calls-to-select-in-bu.patch
Requires: CSMT patches.

Can reduce CPU usage when using the CSMT patchset by up to 50% or sometimes even more. Whether this translates into
an FPS increase or an improvement in responsiveness depends on your OS and hardware (and game).

### 0004-wine-list.h-linked-list-cache-line-prefetching.patch, 0005-ntdll-heap.c-freelist_balance-prefetch-next-entry-ca.patch, 0006-oleaut32-typelib.c-fix-cursor2-having-the-wrong-type.patch
Potentially doubles the speed at which linked-list can be traversed. Linked lists are used in many places in wine.
Patch 0005 is only needed if you are also using the heap allocation patch (0001).
