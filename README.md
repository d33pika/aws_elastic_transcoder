aws_elastic_transcoder
======================

Script to generate aws4 signature to make GET and POST requests to AWS elastic transcoder. I extracted the aws4 signing logic from aws-sdk ruby gem.

Example usage:
A job Post request:
````` ruby
params = {
  "Input" => {
    "Key" => key,
    "FrameRate" => "auto",
    "Resolution" => "auto",
    "AspectRatio" => "auto",
    "Interlaced" => "auto",
    "Container" => "auto"
  },
  "Output"=> {
    "Key" => output_key,
    "ThumbnailPattern" => "",
    "Rotate" => "auto",
    "PresetId" => preset_id
    },
    "PipelineId" => pipeline_id
  }

  body = JSON.generate(params)
  request_type = "POST"
  qs = nil
  path = "/2012-09-25/jobs"
  ETS.new(request_type, qs, body, path).post_request
`````
A get Jobs request:

````` ruby
  body = nil
  request_type = "GET"
  qs = 'Ascending=true'
  path = "/2012-09-25/jobsByPipeline/#{pipeline_id}"
  next_page = ETS.new(request_type, qs, body, path).get_request
`````
