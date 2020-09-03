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
