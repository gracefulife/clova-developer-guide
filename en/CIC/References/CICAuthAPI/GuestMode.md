### Remarks
 To provide guest mode service to users without {{book.TargetServiceForClientAuth}} account authentication, follow below steps.

1. From [Creating Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken) procedure description, skip step 1 and 2.
2. When [request for authorization code](#RequestAuthorizationCode) from step 3, apply the following two.
  * Do not enter `Authorization` field on the requested headers.
  * Add `request_vu` as query parameter and set as `Y`.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The basic value of <code>request_vu</code> is <code>N</code> and the basic policy is to authorize {{ book.TargetServiceForClientAuth }} account for usage.</p>
</div>

By following the above, authorization code for guest mode will be acquired. Process the rest of steps explained on [Create Clova access token](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken) with the guest code to obtain Clova access token for guests.

Below is an example of requesting for guest mode authorization code.

<pre><code>$ curl {{ book.AuthServerBaseURL }}authorize \
       --data-urlencode 'request_vu=Y' \
       --data-urlencode 'client_id=c2Rmc2Rmc2FkZ2Fasdkjh234zZnNhZGZ' \
       --data-urlencode 'device_id=aa123123d6-d900-48a1-b73b-aa6c156353206' \
       --data-urlencode 'model_id=test_model' \
       --data-urlencode 'response_type=code' \
       --data-urlencode 'state=FKjaJfMlakjdfTVbES5ccZ'
</code></pre>