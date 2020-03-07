Django Hybrid Router
=========

A more flexible router to django rest framework. It allows to register simple API views in the router and merge multiple routers in a base one.


## Install

```pip install git+ssh://git@bitbucket.org/hub9/django-hybrid-router```


## Usage

```
#!python
# urls.py

from hybridrouter import HybridRouter
...

class CarViewSet(viewsets.ModelViewSet):
    ...

class DriverViewSet(viewsets.ModelViewSet):
    ...

@api_view(['POST'])
def drive_car_view(request):
    ...

router1 = HybridRouter()
# Register ViewSet
router1.register(r'car', CarViewSet)
# Register View
router1.add_api_view('drive_car', url(r'^drive_car/$', drive_car_view, name='drive-car'))

router2 = HybridRouter()
# Register ViewSet
router2.register(r'driver', DriverViewSet)

main_router = HybridRouter()
# Group routers registers in a single main router
main_router.register_router(router1)
main_router.register_router(router2)

urlpatterns = [
    ...
    url(r'^api/', include(main_router.urls)),
    ...
]
```

Accesing 'api/' url will show Django rest framework page listing 'car', 'drive_car' and 'driver' endpoints.


Fork from [Django Hybrid Router](https://bitbucket.org/hub9/django-hybrid-router)
