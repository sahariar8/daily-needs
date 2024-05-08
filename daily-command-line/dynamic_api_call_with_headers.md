~~~~~~
  public function details(Request $request, $drugName){
        $url = sprintf(LaravelConfig::get('nih.fdb_dispensable_Drug_api_to_get_drug_id_by_drugName'), $drugName, LaravelConfig::get('nih.fdb_clientID'));
        $headers = [
        'Authorization' => 'SHAREDKEY ' . LaravelConfig::get('nih.fdb_clientID') . ':' . LaravelConfig::get('nih.api_access_key'),
        'Accept' => 'application/json',
        ];

        $response = Http::withHeaders($headers)->get($url);
        $dispensableDrugs = $response->json();
        return view('drugDetails',['trades' => $dispensableDrugs]);
       
    }
~~~~~~