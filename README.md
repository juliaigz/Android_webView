# Android_webView
### This is an Android Studio project made in java and xml, using fragments, to show an url. 

The XML of the main activity
![image](https://github.com/juliaigz/Android_webView/assets/40221707/47f0f955-7a5b-4aac-8313-85f594452964)

The XML of the fragment
![image](https://github.com/juliaigz/Android_webView/assets/40221707/ab5749c1-a1a4-466f-b27e-81c6e27dab6e)


we use one Fragment and a mainActivity
![image](https://github.com/juliaigz/Android_webView/assets/40221707/1ebe2018-83d9-4563-a781-807fb7833be5)

the code of the main Activity 

´´´Bash

public class MainActivity extends AppCompatActivity {
   private ActivityMainBinding mbinding;
   private EditText editText1;
   private Button button1;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //setContentView(R.layout.activity_main);

        mbinding = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(mbinding.getRoot());

        editText1 = mbinding.editText1;
        button1 = mbinding.button1;

        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                mostrarFragmento();
            }
        });
    }
    private void mostrarFragmento() {
        // Crea una instancia del fragmento MessageFragment
        BlankFragment fragment = BlankFragment.newInstance(editText1.getText().toString());
        // Obtiene el administrador de fragmentos
        FragmentManager fragmentManager = getSupportFragmentManager();
        // Inicia una transacción de fragmento
        FragmentTransaction transaction = fragmentManager.beginTransaction();
        // Reemplaza el contenido del contenedor con el fragmento MessageFragment
        transaction.replace(mbinding.container.getId(), fragment);
        // Opcional: añade la transacción a la pila de retroceso
        transaction.addToBackStack(null);
        // Realiza la transacción
        transaction.commit();
    }
}

´´´


The code of the Fragment


´´´Bash

public class BlankFragment extends Fragment {
    // TODO: Rename parameter arguments, choose names that match
    // the fragment initialization parameters, e.g. ARG_ITEM_NUMBER
    private static final String ARG_PARAM1 = "param1";
    // TODO: Rename and change types of parameters
    private String mParam1;
    private WebView webView1;
    public BlankFragment() {
        // Required empty public constructor
    }
    /**
     * Use this factory method to create a new instance of
     * this fragment using the provided parameters.
     *
     * @param param1 Parameter 1.
     * @return A new instance of fragment BlankFragment.
     */
    // TODO: Rename and change types and number of parameters
    public static BlankFragment newInstance(String param1) {
        BlankFragment fragment = new BlankFragment();
        Bundle args = new Bundle();
        args.putString(ARG_PARAM1, param1);
        fragment.setArguments(args);
        return fragment;
    }
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        if (getArguments() != null) {
            mParam1 = getArguments().getString(ARG_PARAM1);
        }
    }
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        View view = inflater.inflate(R.layout.fragment_blank, container, false);

        webView1 = view.findViewById(R.id.webview1);
        webView1.getSettings().setJavaScriptEnabled(true);
        webView1.setWebViewClient(new WebViewClient());
        webView1.loadUrl(mParam1);
        return view;
    }
}


´´´

