### MMS 문자 전송 소스코드
``` java
private void SendMMS(Context context, ArrayList<String> urlString) {
		boolean exceptionCheck = false;

		Intent sendIntent = new Intent();

		// Selection count
		if (urlString.size() > 1) {
			sendIntent.setAction(Intent.ACTION_SEND_MULTIPLE);

		} else if (urlString.size() == 1) {
			sendIntent.setAction(Intent.ACTION_SEND);
		} else {
			Toast.makeText(this, "Please Check the Image.", Toast.LENGTH_LONG)
					.show();
			exceptionCheck = true;
		}

		if (!exceptionCheck) {
			sendIntent.setData(Uri.parse("mmsto:"));
			sendIntent.addCategory("android.intent.category.DEFAULT");

			ArrayList<Uri> uris = new ArrayList<Uri>();

			for (String file : urlString) {
				File fileIn = new File("file://" + file);
				Uri u = Uri.fromFile(fileIn);
				uris.add(u);
			}
			sendIntent.setType("image/jpeg");

			if (urlString.size() > 1) {
				sendIntent.putParcelableArrayListExtra(Intent.EXTRA_STREAM,
						uris);

			} else {
				sendIntent.putExtra(Intent.EXTRA_STREAM,
						Uri.parse("file://" + urlString.get(0)));
			}

		}

		try {
			startActivity(sendIntent);

		} catch (Exception e) {
			Toast.makeText(this, "Send Failed..", Toast.LENGTH_LONG).show();

		}
     }

```
> 출처: http://mashroom.tistory.com/17 [MashRoom]
