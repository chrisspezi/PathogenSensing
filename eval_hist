function GradientHist
    h=figure('Position',[50,200,1800,800]);

    button1 = uicontrol('Style', 'pushbutton', ...
        'String', 'select Gradient Data 1',...
        'Position', [120 60 150 40],...
        'Callback', @GetfileA); 
  
    button2 = uicontrol('Style', 'pushbutton', ...
        'String', 'Start',...
        'Position', [1300 20 180 60],...
        'Callback', @Analyse);
    button3= uicontrol('Style', 'pushbutton', 'String', 'Clear',...
        'Position', [1500 20 180 60],...
        'Callback', 'cla'); 
    
    button4 = uicontrol('Style', 'pushbutton', ...
        'String', 'select Gradient Data 2',...
        'Position', [350 60 150 40],...
        'Callback', @GetfileB); 
    
    
    textUpper=uicontrol('Style','text',...
        'Position',[850 40 160 40],...
        'String','Upper Input');
    
    Upper = uicontrol('Style', 'edit', ...
        'String', '1e-6',...
        'Position', [850 20 160 40]);
    
    textLower=uicontrol('Style','text',...
        'Position',[650 40 160 40],...
        'String','Lower Input');
    
    Lower = uicontrol('Style', 'edit', ...
        'String', '0',...
        'Position', [650 20 160 40]);
    
    textBin=uicontrol('Style','text',...
        'Position',[1050 40 160 40],...
        'String','Bin Number');
    
    BinNum = uicontrol('Style', 'edit', ...
        'String', '100',...
        'Position', [1050 20 160 40]);
    
    
        
    
    axis1 = axes('Units' , 'pixels' , 'Position',[70 150 800 600]);
    axis2 = axes('Units' , 'pixels' , 'Position',[950 150 800 600]);
    

    
    function GetfileA(~ ,~)
        %choose the file that you would analyse
        [name,path]=uigetfile('~.mat');
        filename = [path,name];
        setappdata(h,'filename1',filename)
        
        textData1=uicontrol('Style','text',...
            'Position',[120 20 150 40],...
            'String',name);
        
        
    end
    
    function GetfileB(~ ,~)
        %choose the file that you would analyse
        [name,path]=uigetfile('~.mat');
        filename = [path,name];
        setappdata(h,'filename2',filename)
        
        textData2=uicontrol('Style','text',...
            'Position',[350 20 150 40],...
            'String',name);
        
        
    end

    function Analyse(~,~)
        
        currentUpper=str2double(get(Upper,'String')); 
        currentLower=str2double(get(Lower,'String')); 
        currentBin=str2double(get(BinNum,'String')); 
        
        %%
        filename1= getappdata(h,'filename1')
        Data_1=importdata(filename1);
        
        Data_1_x = Data_1(:,1);
        Data_1_y = Data_1(:,2);
        Data_1_z = Data_1(:,3);
        Data_1_value = Data_1(:,4);
        
        [m,n]=find(isnan(Data_1));
        
        Invalid_data_1=Data_1(m,:);
        Data_1(m,:)=[];
        
        k=find(Data_1(:,4)<=0 | Data_1(:,4)>=5e-6 );
        Overrange_Data_1=Data_1(k,:);
        
        Data_1(k,:)=[];
        Data_1_opt=Data_1;
        
        
        x1 = Data_1_opt(:,1);
        y1= Data_1_opt(:,2);
        z1= Data_1_opt(:,3);
        v1= Data_1_opt(:,4);
        
        %%
        filename2= getappdata(h,'filename2')
        Data_2=importdata(filename2);
        
        [m,n]=find(isnan(Data_2));
        
        Invalid_data_2=Data_2(m,:);
        Data_2(m,:)=[];
        
        k=find(Data_2(:,4)<=0 | Data_2(:,4)>=5e-6 );
        Overrange_Data_2=Data_2(k,:);
        
        Data_2(k,:)=[];
        Data_2_opt=Data_2;
        
        
        x2 = Data_2_opt(:,1);
        y2 = Data_2_opt(:,2);
        z2= Data_2_opt(:,3);
        v2= Data_2_opt(:,4);
        %%
        set (h,'CurrentAxes',axis1);
        edges = linspace(currentLower,currentUpper,currentBin);
        hist = histogram(v1);
        hist.NumBins=currentBin;
        hist.BinEdges = [edges (currentUpper+1e-6)];
        hist.Normalization = 'countdensity';

        
        title('Gradient1')
        ylabel('Count');
        xlabel('Value');
        hold on
        
        set (h,'CurrentAxes',axis2);
        
        
   
        edges = linspace(currentLower,currentUpper,currentBin);
        hist = histogram(v2);
        hist.NumBins=currentBin;
        hist.BinEdges = [edges (currentUpper+1e-6)];
        hist.Normalization = 'countdensity';
        
        title('Gradient2')
        ylabel('Count');
        xlabel('Value');
        hold on
        
        
        
        
       hold on  
        
      end


end
