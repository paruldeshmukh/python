# python
class FileView(APIView):
  serializer_class = FileSerializer
  parser_classes = (MultiPartParser, FormParser)

  def post(self, request, *args, **kwargs):

    file_serializer = FileSerializer(data=request.data,partial =True)
    if file_serializer.is_valid():
      file_serializer.save()
      
      return Response(file_serializer.data, status=status.HTTP_201_CREATED)
    else:
      return Response(file_serializer.errors, status=status.HTTP_400_BAD_REQUEST)

