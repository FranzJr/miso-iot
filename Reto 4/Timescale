#Explicación del ajuste
Vamos a crear un nuevo endpoint que devuelve la suma total de valores (value) para una medida específica (measurement) de todas las estaciones (station) dentro de un rango de tiempo específico. Esta suma nos puede dar una idea de cuánto se ha medido una determinada entidad en todas las estaciones durante un período de tiempo.

##Endpoint
http://184.73.130.220:8000/totalMeasurement/Temperatura/?from=1622523600000&to=1698814799999
http://184.73.130.220:8000/totalMeasurement/Humedad/?from=1622523600000&to=1698814799999

##Postgres
SELECT SUM(value) FROM Data 
WHERE measurement_id = :selectedMeasurementId AND time BETWEEN :start AND :end;

##Función
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
