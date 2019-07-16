### How to launch job using Curl

Launching a job template from command line using Curl.  Passing extra_vars in the body.  Make sure extra variables "Prompt on launch" is enabled, so extra_vars can be passed.

```shell
curl -f -k -H 'Content-Type: application/json' -H 'Authorization: Bearer YF6pz330n7MjOGiZ5mQEM0024X6Ut7' -XPOST -d '{"extra_vars": "{\"hello\": \"world\"}" }' https://tower.lab.home/api/v2/job_templates/497/launch/
```