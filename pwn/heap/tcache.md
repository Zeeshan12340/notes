# tcache
thread local caching is used to speed up small allocations in a single thread, implemented as a singly-linked list with each thread having a list header for different-sized allocations. Different sized allocations go to different lists. 

Until you free something, tcache doesn't come into play. When you free something you put an entry into the cache, same sized allocations create a single linked list.