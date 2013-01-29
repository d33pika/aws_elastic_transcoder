aws_elastic_transcoder
======================

Script to generate aws4 signature to mage get and post requests to AWS elastic transcoder. I extracted the aws4 logic from aws-sdk ruby gem.

Example usage:
A job Post request:

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
  path = "/xxx/jobs"
  ETS.new(request_type, qs, body, path).post_request

A get Jobs request:

  body = nil
  request_type = "GET"
  qs = 'Ascending=true'
  path = "/xxx/jobsByPipeline/#{pipeline_id}"
  next_page = ETS.new(request_type, qs, body, path).get_request
