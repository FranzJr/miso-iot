# Explicación del ajuste TIMESCALE
Vamos a crear un nuevo endpoint que devuelve la suma total de valores (value) para una medida específica (measurement) de todas las estaciones (station) dentro de un rango de tiempo específico. Esta suma nos puede dar una idea de cuánto se ha medido una determinada entidad en todas las estaciones durante un período de tiempo.

## Endpoint
http://184.73.130.220:8000/totalMeasurement/Temperatura/?from=1622523600000&to=1698814799999
http://184.73.130.220:8000/totalMeasurement/Humedad/?from=1622523600000&to=1698814799999

## Postgres
SELECT SUM(value) FROM Data 
WHERE measurement_id = :selectedMeasurementId AND time BETWEEN :start AND :end;

## Función
```python
def get_total_measurement(request, **kwargs):
    data_result = {}

    measureParam = kwargs.get("measure", None)
    selectedMeasure = Measurement.objects.filter(name=measureParam).first()

    if not selectedMeasure:
        return JsonResponse({"error": "Medida no encontrada"}, status=404)

    try:
        start = datetime.fromtimestamp(float(request.GET.get("from", None)) / 1000)
    except:
        start = None

    try:
        end = datetime.fromtimestamp(float(request.GET.get("to", None)) / 1000)
    except:
        end = None

    if start == None and end == None:
        start = datetime.now()
        start = start - dateutil.relativedelta.relativedelta(weeks=1)
        end = datetime.now()
        end += dateutil.relativedelta.relativedelta(days=1)
    elif end == None:
        end = datetime.now()
    elif start == None:
        start = datetime.fromtimestamp(0)

    # Convert datetime objects back to timestamps
    start_timestamp = int(start.timestamp() * 1000000)
    end_timestamp = int(end.timestamp() * 1000000)

    total_value = Data.objects.filter(
        measurement=selectedMeasure,
        time__range=(start_timestamp, end_timestamp)  # Use timestamps here
    ).aggregate(total_value=Sum("avg_value"))
```

# Explicación del ajuste POSTGRES
Vamos a crear un nuevo endpoint que devuelve la suma total de valores (value) para una medida específica (measurement) de todas las estaciones (station) dentro de un rango de tiempo específico. Esta suma nos puede dar una idea de cuánto se ha medido una determinada entidad en todas las estaciones durante un período de tiempo.

## Endpoint
http://54.227.102.228:8000/totalMeasurement/Temperatura/?from=1622523600000&to=1698814799999
http://54.227.102.228:8000/totalMeasurement/Humedad/?from=1622523600000&to=1698814799999


## Función
```python
def get_total_measurement(request, **kwargs):
    data_result = {}

    measureParam = kwargs.get("measure", None)
    selectedMeasure = Measurement.objects.filter(name=measureParam).first()

    if not selectedMeasure:
        return JsonResponse({"error": "Medida no encontrada"}, status=404)

    try:
        start = datetime.fromtimestamp(float(request.GET.get("from", None)) / 1000)
    except:
        start = None

    try:
        end = datetime.fromtimestamp(float(request.GET.get("to", None)) / 1000)
    except:
        end = None

    if start == None and end == None:
        start = datetime.now()
        start = start - dateutil.relativedelta.relativedelta(weeks=1)
        end = datetime.now()
        end += dateutil.relativedelta.relativedelta(days=1)
    elif end == None:
        end = datetime.now()
    elif start == None:
        start = datetime.fromtimestamp(0)

    total_value = Data.objects.filter(
        measurement=selectedMeasure,
        time__date__range=(start.date(), end.date())
    ).aggregate(total_value=Sum("value"))

    data_result["measure"] = selectedMeasure.name
    data_result["total_value"] = total_value["total_value"] if total_value["total_value"] else 0
    data_result["start"] = start.strftime("%d/%m/%Y")
    data_result["end"] = end.strftime("%d/%m/%Y")

    return JsonResponse(data_result)

