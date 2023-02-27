# Applying-Kalman-Filtering-to-a-List-of-Data-with-Error
Applying Kalman Filter to a List of Data with Error
randomDataCountForTest = 5000;
dataWithError          = [];
%% CALCULATE STANDARD DEVIATION OF MEASUREMENT WITH ERROR %%
c9 = std(dataWithError);
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
z(:,1) = 0;
for m = 1:randomDataCountForTest
    z(:,m+1) = dataWithError(m);
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
H = 1;
F = 1;
G = 1;
u = 0;
N = length(z);
R = c9;
I = 1;
Q = 0;

x(:, 1) = 0;

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

P = 1;

for k= 2:N
    x(:, k) = F*x(:, k-1) + G*u;
    P = F*P*F' + Q;
    K = P*H' / (H*P*H' + R);
    x(:,k) = x(:,k) + K*(z(k) - H*x(:,k));
    P = (I - K*H)*P;
end

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
disp(x);
plot(x);
