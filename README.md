# Custom-View


<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">

    <androidx.constraintlayout.widget.ConstraintLayout
        android:id="@+id/referenceIdLayout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@android:color/transparent">


        <androidx.appcompat.widget.AppCompatTextView
            android:id="@+id/headingLabelTv"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:gravity="start"
            android:text="@string/enter_reference_number"
            android:textColor="@color/a333333"
            app:layout_constraintBottom_toTopOf="@+id/contentMainView"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent"
            app:layout_constraintVertical_bias="0" />

        <androidx.constraintlayout.widget.ConstraintLayout
            android:id="@+id/contentMainView"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="@dimen/_4sdp"
            android:background="@drawable/input_border"
            android:foreground="?android:attr/selectableItemBackground"
            android:visibility="visible"
            app:layout_constraintBottom_toTopOf="@+id/bottomLabelTv"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/headingLabelTv"
            app:layout_constraintVertical_bias=".0">

            <View
                android:id="@+id/verticalBar"
                android:layout_width="@dimen/_6sdp"
                android:layout_height="0dp"
                android:background="@color/colorPrimary_New"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintHorizontal_weight="1"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent" />


            <androidx.appcompat.widget.AppCompatEditText
                android:id="@+id/referenceIdEt"
                android:layout_width="0dp"
                android:layout_height="0dp"
                android:layout_centerVertical="true"
                android:background="@null"
                android:hint="@string/referenceNumber_hint"
                android:imeOptions="actionDone"
                android:inputType="number"
                android:maxLength="25"
                android:singleLine="true"
                android:maxLines="1"
                android:focusable="false"
                android:editable="false"
                android:enabled="false"
                android:paddingStart="@dimen/_6dp"
                android:textColor="@color/a333333"
                android:textSize="@dimen/_14ssp"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toStartOf="@+id/iconView"
                app:layout_constraintStart_toEndOf="@+id/verticalBar"
                app:layout_constraintTop_toTopOf="parent" />


            <androidx.appcompat.widget.AppCompatImageView
                android:id="@+id/iconView"
                android:layout_width="@dimen/_32sdp"
                android:layout_height="@dimen/_32sdp"
                android:layout_margin="@dimen/_6sdp"
                android:background="@drawable/bill_sample_ic"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintStart_toEndOf="@+id/referenceIdEt"
                app:layout_constraintTop_toTopOf="parent" />


        </androidx.constraintlayout.widget.ConstraintLayout>

        <androidx.appcompat.widget.AppCompatTextView
            android:id="@+id/bottomLabelTv"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginTop="@dimen/_4sdp"
            android:text="@string/view_your_reference_number"
            android:textColor="@color/colorPrimary_New"
            android:textSize="@dimen/_10ssp"
            app:layout_constraintBottom_toTopOf="@+id/errorLabelTv"
            app:layout_constraintEnd_toEndOf="parent"

            app:layout_constraintTop_toBottomOf="@+id/contentMainView" />


        <androidx.appcompat.widget.AppCompatTextView
            android:id="@+id/errorLabelTv"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginTop="@dimen/_6sdp"
            android:gravity="start"
            android:textColor="#ca1305"
            android:textSize="@dimen/_10ssp"
            android:visibility="visible"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/bottomLabelTv"
            tools:text="@string/ubp_your_reference_number_is_incorrect" />


    </androidx.constraintlayout.widget.ConstraintLayout>

</layout>


    <declare-styleable name="ContentViewWithImage">
        <attr name="android:inputType" />
        <attr name="android:imeOptions" />
        <attr name="android:maxLines" />
        <attr name="android:textSize" />
        <attr name="android:minLines" />
        <attr name="android:maxLength" />
        <attr name="android:digits" />
        <attr name="android:hint" />
        <attr name="android:singleLine" />
        <attr name="headerLabelText" />
        <attr name="footerLabelText" />
        <attr name="errorMessage" />
        <attr name="errorColor" />
    </declare-styleable>



class ContentViewWithImage : ConstraintLayout {


    //views
    var headerLabel: AppCompatTextView? = null
    var footerLabel: AppCompatTextView? = null
    var errorLabel: AppCompatTextView? = null
    var contentEditText: AppCompatEditText? = null
    var iconView: AppCompatImageView? = null
    var errorVerticalBar: View? = null
    var contentMainView: ConstraintLayout? = null


    //values


    var imeOptions = -1
    var contentHintText = ""
    var contentHeaderText = ""
    var contentFooterText = ""
    var contentErrorText = ""
    var contentErrorLabelColor = Color.RED
    var contentErrorLabelTextSize = 8
    var digits: String? = null
    var inputType = 0

    var maxLength = 14
    var minLength = 0


    //Primary Constructor
    constructor(context: Context) : super(context)

    //Secondary Constructor
    constructor(context: Context, attrs: AttributeSet?) : super(context, attrs) {
        try {
            initView(context, attrs) //init view
        } catch (ignored: Exception) {
            ignored.message
        }

    }

    private fun initView(@NonNull context: Context, @NonNull attrs: AttributeSet?) {
        //inflating view
        inflate(context, R.layout.edittext_with_image, this)
        // setting background to transparent
        setBackgroundColor(Color.TRANSPARENT)

        headerLabel = findViewById(R.id.headingLabelTv)
        footerLabel = findViewById(R.id.bottomLabelTv)
        errorLabel = findViewById(R.id.errorLabelTv)
        contentEditText = findViewById(R.id.referenceIdEt)

        iconView = findViewById(R.id.iconView)
        errorVerticalBar = findViewById(R.id.verticalBar)
        contentMainView = findViewById(R.id.contentMainView)


        initAttrs(attrs)


    }

    private fun initAttrs(@NonNull attrs: AttributeSet?) {

        val typedArray = context.obtainStyledAttributes(attrs, R.styleable.ContentViewWithImage)

        if (null != typedArray) {

            imeOptions = typedArray.getInt(R.styleable.ContentViewWithImage_android_hint, -1)

            contentHintText = typedArray.getString(R.styleable.ContentViewWithImage_android_hint)!!

            contentHeaderText = typedArray.getString(R.styleable.ContentViewWithImage_headerLabelText)!!

            contentFooterText = typedArray.getString(R.styleable.ContentViewWithImage_footerLabelText)!!

            contentErrorText = typedArray.getString(R.styleable.ContentViewWithImage_errorMessage)!!

            contentErrorLabelColor = typedArray.getInt(R.styleable.ContentViewWithImage_errorColor, Color.RED)

     //            contentErrorLabelTextSize = typedArray.getInt(R.styleable.ContentViewWithImage_, 8)


            typedArray.recycle()
        }

    }

 
     }

//Java Widget



package pk.com.telenor.phoenix.widget;

import android.annotation.SuppressLint;
import android.content.Context;
import android.content.res.TypedArray;
import android.graphics.Color;
import android.os.Build;
import android.text.Editable;
import android.text.InputFilter;
import android.text.InputType;
import android.text.TextUtils;
import android.text.TextWatcher;
import android.text.method.DigitsKeyListener;
import android.util.AttributeSet;
import android.util.Log;
import android.view.ActionMode;
import android.view.KeyEvent;
import android.view.Menu;
import android.view.MenuItem;
import android.view.inputmethod.EditorInfo;
import android.view.inputmethod.InputMethodManager;
import android.widget.ImageView;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.constraintlayout.widget.ConstraintLayout;
import androidx.lifecycle.Lifecycle;

import com.google.android.material.textfield.TextInputEditText;
import com.google.android.material.textfield.TextInputLayout;
import com.uber.autodispose.AutoDispose;
import com.uber.autodispose.android.lifecycle.AndroidLifecycleScopeProvider;

import java.util.concurrent.TimeUnit;

import io.reactivex.Observable;
import io.reactivex.android.schedulers.AndroidSchedulers;
import pk.com.telenor.phoenix.R;
import pk.com.telenor.phoenix.utils.MathUtil;
import pk.com.telenor.phoenix.utils.RuleUtils;
import pk.com.telenor.phoenix.utils.ServicesUtils;


/**
 * @Author Muhammad Atif Arif
 * @Github atifabbasi19
 */


public class NewContentInputView extends ConstraintLayout {


    String inputResult = "";
    ImageView clearButton;
    ImageView keyBoardButton;
    TextView errorTextView;

    TextInputLayout textInputLayout;
    TextInputEditText editText;


    TextView
            rsLabel;

    String hintText = " ";
    int imeOptions = -1;
    String contentExample = "";
    String digits = null;

    int inputType;

    String textViewErrorMessage = "Invalid input";
    int errorMessageColor = Color.RED;

    boolean isAmount = false;
    boolean isWallet = false;

    int max = -1;
    int min = -1;


    AddEditTextChangedListener textChangedListener = null;


    public void setText(String input) {

        if (input != null && input.length() > 0) {
            editText.setText(input);
        }

        updateInputUI();


    }

    private void updateInputUI() {

        boolean hasText = false;

        hasText = editText.getText() != null && editText.getText().length() > 0;

        if (hasText) {
            clearButton.setVisibility(VISIBLE);
            keyBoardButton.setVisibility(GONE);

        } else {
            clearButton.setVisibility(GONE);
            keyBoardButton.setVisibility(VISIBLE);
        }
/*
        if (isAmount && hasText) {
            updateRs(true);
        } else {
            updateRs(false);
        }*/

    }

    public NewContentInputView(Context context, AttributeSet attrs) {
        super(context, attrs);
        // TODO: 8/17/2019 remove try catch after Completing development
        try {
            init(context, attrs);
        } catch (Exception ignored) {
            ignored.getMessage();
        }

    }


    private void init(@NonNull Context context, @NonNull AttributeSet attrs) {

        inflate(context, R.layout.custom_material_edit_text, this);

        setBackgroundColor(Color.TRANSPARENT);


        textInputLayout = findViewById(R.id.textInputLayout);

        rsLabel = findViewById(R.id.rsLabel);
        rsLabel.setVisibility(GONE);

        editText = findViewById(R.id.textInputEditText);

        clearButton = findViewById(R.id.cancelButton);

        keyBoardButton = findViewById(R.id.keyboardButton);

        errorTextView = findViewById(R.id.errorTextView);


        TypedArray typedArray = context.obtainStyledAttributes(attrs, R.styleable.NewContentInputView);

        if (typedArray != null) {


            hintText = typedArray.getString(R.styleable.NewContentInputView_android_hint);
            imeOptions = typedArray.getInt(R.styleable.NewMobileInputView_android_imeOptions, EditorInfo.IME_ACTION_DONE);

            contentExample = typedArray.getString(R.styleable.NewMobileInputView_editTextHint);
            textViewErrorMessage = typedArray.getString(R.styleable.NewContentInputView_textViewErrorMessage);
            errorMessageColor = typedArray.getColor(R.styleable.NewContentInputView_textViewErrorColor, errorMessageColor);
            inputType = typedArray.getColor(R.styleable.NewContentInputView_android_inputType, InputType.TYPE_NULL);

            isAmount = typedArray.getBoolean(R.styleable.NewContentInputView_android_inputType, isAmount);
            isWallet = typedArray.getBoolean(R.styleable.NewContentInputView_android_inputType, isWallet);
            digits = typedArray.getString(R.styleable.NewContentInputView_android_digits);


  /*          editTextSize = typedArray.getDimensionPixelSize(R.styleable.MaterialEditText_android_textSize, 12);
            errorTextSize = typedArray.getDimensionPixelSize(R.styleable.MaterialEditText_errorTextSize, 12);
            //TypedValue.COMPLEX_UNIT_PX,
            if (editTextSize > 0) {
                editText.setTextSize(editTextSize);
            }

            if (errorTextSize > 0) {
                errorTextView.setTextSize(errorTextSize);
            }
*/

            typedArray.recycle();
        }

        errorTextView.setTextColor(errorMessageColor);
        editText.setImeOptions(imeOptions);

        textInputLayout.setHint(hintText);

        if (editText.getInputType() == InputType.TYPE_CLASS_PHONE) {
            editText.setKeyListener(DigitsKeyListener.getInstance("0123456789+"));
            editText.setFilters(new InputFilter[]{new InputFilter.LengthFilter(17)});
        }

        editText.setLongClickable(false);
        editText.setTextIsSelectable(false);

        if (digits != null) {
            editText.setKeyListener(DigitsKeyListener.getInstance(digits));
        }


        textInputLayout.setHint(hintText);
        editText.setInputType(inputType);

        errorTextView = findViewById(R.id.errorTextView);
        errorTextView.setText(" " + textViewErrorMessage);
        errorTextView.setTextColor(errorMessageColor);
        errorTextView.setVisibility(GONE);


        /**
         * Setting EditText to Empty
         * @inputResult String that returns editText value
         * */
        clearButton.setOnClickListener(view -> {
            editText.setText("");
//            updateRs(false);
            inputResult = "";
        });

        keyBoardButton.setOnClickListener(view -> {
            showKeyBoard(getContext());
        });


        editText.addTextChangedListener(new TextWatcher() {
            @Override
            public void beforeTextChanged(CharSequence s, int start, int count, int after) {

                if (textChangedListener != null) {
                    textChangedListener.beforeTextChanged(s, start, count, after);
                }

            }

            @Override
            public void onTextChanged(CharSequence s, int start, int before, int count) {

                editText.setSelection(s.length());

                if (textChangedListener != null) {
                    textChangedListener.onTextChanged(s, start, before, count);
                }

                String enteredString = s.toString();
                if (!isWallet) {
                    if (enteredString.startsWith("0"))
                        editText.setText("");
                }

                Log.d("test", "onTextChanged:" + s.toString());


            }

            @Override
            public void afterTextChanged(Editable s) {


                int BORDER_STROKE_GREY = getResources().getColor(R.color.border_stroke_grey);

                textInputLayout.setBoxStrokeColor(BORDER_STROKE_GREY);


                Log.d("test", "afterTextChanged" + editText.getText().toString());

                if (s.length() == 0)
                    keyBoardButton.setVisibility(VISIBLE);
                errorTextView.setVisibility(GONE);

                if (s.length() > 0 && editText.isEnabled()) {
                    clearButton.setVisibility(VISIBLE);
                    keyBoardButton.setVisibility(GONE);
                }

                if (s.length() > 0 && editText.hasFocus() && editText.isEnabled()) {
                    clearButton.setVisibility(VISIBLE);
                    keyBoardButton.setVisibility(GONE);
                } else {
                    keyBoardButton.setVisibility(VISIBLE);
                    clearButton.setVisibility(GONE);
                }
                if (listener != null) {
                    listener.onMobileNoChange(s);
                }


                if (textChangedListener != null) {
                    textChangedListener.afterTextChanged(s);
                }
            }
        });
        editText.setOnFocusChangeListener((v, f) -> {

            if (f) {
                showKeyBoard(getContext());
                editText.setHint(contentExample.equals("0x6") ? "" : contentExample);
//                updateRs(true);
            } else {
                editText.setHint("");
              /*  if (editText.getText() != null && editText.getText().length() > 0) {
                    updateRs(true);
                } else {
                    updateRs(false);
                }*/

            }


            if (f && editText.getText().length() > 0 && editText.isEnabled()) {
                keyBoardButton.setVisibility(GONE);
                clearButton.setVisibility(VISIBLE);
            } else {
                clearButton.setVisibility(GONE);
            }
        });
        editText.setOnEditorActionListener(new TextView.OnEditorActionListener() {
            @Override
            public boolean onEditorAction(TextView v, int actionId, KeyEvent event) {
                try {
                    if (keyBoardChangeListener != null) {
                        keyBoardChangeListener.onKeyBoardNoChange(actionId);
                    }
                } catch (Exception e) {
                }
                return false;
            }
        });

        setOnClickListener(v -> showKeyBoard(getContext()));
        init();


    }

    private void updateRs(boolean update) {

        if (isAmount && update) {
            rsLabel.setVisibility(VISIBLE);
            editText.setX(getResources().getDimension(R.dimen.amountFiledPadding_30dp));
        } else {
            rsLabel.setVisibility(GONE);
            editText.setX(0);
        }

       /* if(editText.hasFocus()){
            rsLabel.setVisibility(VISIBLE);
            editText.setX(getResources().getDimension(R.dimen.amountFiledPadding_30dp));
        }else{
            rsLabel.setVisibility(GONE);
            editText.setX(0);
        }*/

    }


    public void setEnabled(boolean enable) {
        editText.setEnabled(enable);
    }

    public void requestFocus(boolean enable) {
        if (enable) {
            editText.requestFocus();
            editText.setFocusable(enable);
        } else {
            editText.setFocusable(enable);
            editText.clearFocus();
        }
    }

    public void setFocus(boolean flag) {
        editText.setFocusable(flag);
        editText.requestFocus();

    }

    public void setHint(String hint) {
        contentExample = hint;
    }

    public void setMinMax(int min, int max) {
        this.max = max;
        this.min = min;
    }


    private MobileChangeListener listener;
    private KeyBoardChangeListener keyBoardChangeListener;


    public interface MobileChangeListener {
        void onMobileNoChange(Editable editable);
    }

    public interface KeyBoardChangeListener {
        void onKeyBoardNoChange(int actionId);
    }

    public void setOnMblNoChangedListener(MobileChangeListener listener) {
        this.listener = listener;
    }

    public void setOnKeyBoardChangedListener(KeyBoardChangeListener keyBoardChangeListener) {
        this.keyBoardChangeListener = keyBoardChangeListener;
    }


    public boolean isMblNo() {
        return RuleUtils.isPhoneNumber(editText.getText().toString());
    }


    public void setContent(String content) {
        editText.setText(content);
        editText.setSelection(content.length());
    }

    public String getContent() {
        return editText.getText().toString();
    }

    public void setEdit(boolean enable) {
        if (enable) {
            editText.setEnabled(true);
        } else {
            editText.setEnabled(false);
        }
    }


    public void setInputFormat(int length, String digits) {
        if (editText != null) {
            editText.setKeyListener(DigitsKeyListener.getInstance(digits));
            editText.setFilters(new InputFilter[]{new InputFilter.LengthFilter(length)});
        }
    }

    public int setInputFormats(String rule, boolean isAmount) {
        int min = 0;
        if (!TextUtils.isEmpty(rule)) {
            String[] split = rule.split("~");
            if (split.length == 2) {
                if (isAmount) {
                    editText.setFilters(new InputFilter[]{new InputFilterMinMax(MathUtil.getInt(split[0]), MathUtil.getInt(split[1]))});
                } else {
                    editText.setFilters(new InputFilter[]{new InputFilter.LengthFilter(MathUtil.getInt(split[1]))});
                }
                min = MathUtil.getInt(split[0]);
            } else {
                if (isAmount) {
                    editText.setFilters(new InputFilter[]{new InputFilterMinMax(0, MathUtil.getInt(split[0]))});
                } else {
                    editText.setFilters(new InputFilter[]{new InputFilter.LengthFilter(MathUtil.getInt(split[0]))});
                }
            }
        }
        return min;
    }


    public void setImage(int iv) {
        keyBoardButton.setImageResource(iv);
    }

    public void setKeyboardVisible(int visible) {
        keyBoardButton.setVisibility(visible);
        clearButton.setVisibility(GONE);
    }

    public void showKeyBoard(Context activity) {
        Observable.timer(200, TimeUnit.MILLISECONDS).observeOn(AndroidSchedulers.mainThread()).as(AutoDispose.autoDisposable(AndroidLifecycleScopeProvider.from((AppCompatActivity) activity, Lifecycle.Event.ON_DESTROY))).subscribe(l -> {
            editText.setFocusable(true);
            editText.setFocusableInTouchMode(true);
            editText.requestFocus();
            ServicesUtils.getInstance().getInputMethodManager().showSoftInput(editText, 0);
        });
    }

    @SuppressLint("CheckResult")
    public void hideKeyBoard() {
        Observable.timer(200, TimeUnit.MILLISECONDS).observeOn(AndroidSchedulers.mainThread()).subscribe(l -> {
//            edMbl.setFocusable(false);
//            edMbl.setFocusableInTouchMode(false);
//            edMbl.clearFocus();
            InputMethodManager imm = ServicesUtils.getInstance().getInputMethodManager();
//            imm.hideSoftInputFromWindow(edMbl, 0);
            imm.hideSoftInputFromWindow(editText.getWindowToken(), 0);

        });
    }

    public void setInputType(int type) {
        editText.setInputType(type);
    }

    private void init() {
        editText.setLongClickable(false);
        editText.setTextIsSelectable(false);
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            editText.setCustomSelectionActionModeCallback(new ActionMode.Callback() {
                @Override
                public boolean onCreateActionMode(ActionMode mode, Menu menu) {
                    return false;
                }

                @Override
                public boolean onPrepareActionMode(ActionMode mode, Menu menu) {
                    return false;
                }

                @Override
                public boolean onActionItemClicked(ActionMode mode, MenuItem item) {
                    return false;
                }

                @Override
                public void onDestroyActionMode(ActionMode mode) {

                }
            });
        }
    }

    public void setInputFilterMax(String min, String max) {
        editText.setFilters(new InputFilter[]{new InputFilterMinMax(min, max)});

    }


    public TextView getErrText() {
        return errorTextView;
    }

    public TextInputLayout getErrorBorder() {
        return textInputLayout;
    }

    public void setErrText(TextView errText) {
        this.errorTextView = errText;
    }


    public void addEditTextChangedListener(AddEditTextChangedListener listener) {
        textChangedListener = listener;
    }

    public void setError(String msg) {
        errorTextView.setText(msg);
        errorTextView.setTextColor(errorMessageColor);
        errorTextView.setVisibility(VISIBLE);
    }

    public void removeError() {
        errorTextView.setText("");
        errorTextView.setVisibility(GONE);
    }

    public void validatedField() {
        int GREEN = getResources().getColor(R.color.border_stroke_green);
        textInputLayout.setBoxStrokeColor(GREEN);
    }

    public interface AddEditTextChangedListener {

        void beforeTextChanged(CharSequence s, int start, int count, int after);

        void onTextChanged(CharSequence s, int start, int before, int count);

        void afterTextChanged(Editable s);
    }

    }

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="@dimen/_4sdp"
    android:layoutDirection="ltr"
    android:orientation="vertical">

    <com.google.android.material.textfield.TextInputLayout
        android:id="@+id/textInputLayout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginStart="@dimen/_8dp"
        android:layout_marginLeft="@dimen/_8dp"
        android:layout_marginEnd="@dimen/_8dp"
        android:layout_marginRight="@dimen/_8dp"
        android:paddingStart="5dp"
        android:paddingLeft="5dp"
        android:textColor="@color/blackk"
        android:textColorHint="@color/blackk"
        android:textStyle="normal"
        app:actionOverflowButtonStyle="@style/AppTheme.TextFloatLabelAppearance"
        app:boxBackgroundMode="outline"
        app:boxStrokeColor="@color/border_stroke_grey"
        app:counterOverflowTextAppearance="@style/AppTheme.TextFloatLabelAppearance"
        app:errorEnabled="false"
        app:errorTextAppearance="@style/error_label"
        app:helperTextEnabled="true"
        app:hintEnabled="true"
        app:hintTextAppearance="@style/text_label"
        app:layout_constraintBottom_toTopOf="@+id/errorTextView"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:hint="@string/EnterMobileNumber">

        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/textInputEditText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@null"
            android:gravity="start"
            android:inputType="phone"
            android:paddingStart="@dimen/_8dp"
            android:paddingTop="@dimen/_10sdp"
            android:paddingEnd="@dimen/inputFieldPadding_36dp"
            android:paddingRight="@dimen/inputFieldPadding_36dp"
            android:paddingBottom="@dimen/_10sdp"
            android:textDirection="anyRtl"
            tools:text="0335510023" />

    </com.google.android.material.textfield.TextInputLayout>

    <!--android:textColor="#666666"-->
    <TextView
        android:id="@+id/rsLabel"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="16dp"
        android:layout_marginLeft="16dp"
        android:text="Rs. "
        android:textColor="@color/hot_offer_price_black"
        android:textSize="16sp"
        android:visibility="gone"
        app:layout_constraintBottom_toBottomOf="@+id/textInputLayout"
        app:layout_constraintLeft_toLeftOf="@+id/textInputLayout"
        app:layout_constraintStart_toStartOf="@+id/textInputLayout"
        app:layout_constraintTop_toTopOf="@+id/textInputLayout"
        app:layout_constraintVertical_bias=".6" />

    <ImageView
        android:id="@+id/cancelButton"
        android:layout_width="@dimen/inputIcon_20dp"
        android:layout_height="@dimen/inputIcon_20dp"
        android:layout_marginEnd="@dimen/iconMargin_16dp"
        android:layout_marginRight="@dimen/iconMargin_16dp"
        android:src="@mipmap/close"
        android:visibility="gone"
        app:layout_constraintBottom_toBottomOf="@+id/textInputLayout"
        app:layout_constraintEnd_toEndOf="@+id/textInputLayout"
        app:layout_constraintTop_toTopOf="@+id/textInputLayout"
        app:layout_constraintVertical_bias=".48" />


    <ImageView
        android:id="@+id/keyboardButton"
        android:layout_width="@dimen/inputIcon_20dp"
        android:layout_height="@dimen/inputIcon_20dp"
        android:layout_marginEnd="@dimen/iconMargin_16dp"
        android:layout_marginRight="@dimen/iconMargin_16dp"
        android:src="@mipmap/label_keyboard"
        android:visibility="visible"
        app:layout_constraintBottom_toBottomOf="@+id/textInputLayout"
        app:layout_constraintEnd_toEndOf="@+id/textInputLayout"
        app:layout_constraintRight_toRightOf="@+id/textInputLayout"
        app:layout_constraintTop_toTopOf="@+id/textInputLayout"
        app:layout_constraintVertical_bias=".48" />

    <TextView
        android:id="@+id/errorTextView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginStart="@dimen/_8dp"
        android:layout_marginLeft="@dimen/_8dp"
        android:layout_marginEnd="@dimen/_8dp"
        android:layout_marginRight="@dimen/_8dp"
        android:textColor="@color/red"
        android:visibility="gone"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textInputLayout"
        tools:text="Invalid data" />

     </androidx.constraintlayout.widget.ConstraintLayout>


   <declare-styleable name="NewContentInputView">
        <attr name="android:inputType" />
        <attr name="android:imeOptions" />
        <attr name="android:maxLines" />
        <attr name="android:textSize" />
        <attr name="android:minLines" />
        <attr name="android:maxLength" />
        <attr name="android:digits" />

        <attr name="editTextPaddingRight" />
        <attr name="editTextPaddingEnd" />
        <attr name="editTextPaddingLeft" />
        <attr name="editTextPaddingStart" />

        <attr name="android:hint" />

        <attr name="editTextHint" />
        <attr name="errorTextSize" />
        <attr name="android:singleLine" />
        <attr name="isAmount" format="boolean" />
        <!--<attr name="hintText" format="string" />-->
        <attr name="editTextRegex" />
        <attr name="editTextMaxLength" />
        <attr name="textViewErrorMessage" />
        <attr name="textViewErrorColor" />
        <attr name="inputFont" format="integer" />
        <attr name="focusColor" format="color" />


    </declare-styleable>


